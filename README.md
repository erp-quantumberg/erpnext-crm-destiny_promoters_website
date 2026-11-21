# Destiny Promoters Website

The `destiny_promoters_website` app provides the Destiny Developers & Promoters
public website. It combines a Vue 3 single-page frontend with a Frappe backend
for property, gallery, newsletter, and contact-enquiry data.

## Features

- Responsive website pages for home, property listings and details, company
  information, construction, interiors, contact, gallery, privacy policy, and
  terms and conditions.
- Property listings supplied by Frappe, including status and featured-project
  filtering, project details, carousel and gallery images, and active amenities.
- Project gallery and image endpoints, with optional project/tag filtering.
- Contact suggestions saved as Frappe records and emailed through Frappe.
- Newsletter subscription records managed in Frappe.
- Search metadata updated for each frontend route.
- Frappe DocTypes for real-estate projects, amenities, galleries, suggestions,
  and newsletter subscriptions.

## Requirements

- A working [Frappe Bench](https://github.com/frappe/bench) environment with a
  Frappe site. Bench must have its configured database and Redis services
  available.
- Python 3.10 or later.
- Node.js and npm (or Yarn) for installing and building the frontend.
- A configured outgoing email account in Frappe if contact suggestions should
  send email.

## Frappe app dependencies

| App | Required | Notes |
| --- | --- | --- |
| Frappe Framework | Yes | Provides the framework and site services; installed and managed by Bench. |
| ERPNext | No | This app uses its own DocTypes and does not depend on ERPNext. |

No additional Frappe apps are declared in `hooks.py`. Frontend libraries are
declared in [`frontend/package.json`](frontend/package.json). The Python app
metadata and development tooling are in [`pyproject.toml`](pyproject.toml).

## Installation

From the bench directory, fetch the app and install it on the target site:

```bash
cd /path/to/your-bench
bench get-app https://github.com/quantumberg2/qdynamics-realestate-frontend-custoom-app
bench --site your-site install-app destiny_promoters_website
```

Replace `your-site` with the site name in your bench. If the app is already
present in `apps/`, skip `bench get-app`.

Install frontend dependencies and build the production assets:

```bash
cd apps/destiny_promoters_website/frontend
npm install
npm run build
```

Then from the bench directory, apply app migrations and refresh generated
assets:

```bash
bench --site your-site migrate
bench build
```

Restart the bench services after installation or deployment:

```bash
bench restart
```

## Development setup

1. Fetch the app and install it on a development site using the installation
   steps above.
2. From the bench directory, start the Frappe development services:

   ```bash
   bench start
   ```

3. In a separate terminal, install frontend dependencies and start Vite:

   ```bash
   cd apps/destiny_promoters_website/frontend
   npm install
   npm run dev
   ```

4. Open the Vite URL shown in the terminal (normally
   `http://localhost:8080`). Vite proxies backend requests to the bench
   webserver. The proxy port is read from
   `sites/common_site_config.json`.

The frontend is built into the app's public assets directory by Vite. Its
history-mode routes are mapped to the SPA entry point in
[`destiny_promoters_website/hooks.py`](destiny_promoters_website/hooks.py).

## Backend API

The app exposes these whitelisted Frappe methods under `/api/method/`:

| Method | Purpose |
| --- | --- |
| `destiny_promoters_website.api.project_api.get_projects` | Fetch active projects; optional `tag` and `status` filters |
| `destiny_promoters_website.api.project_api.get_project` | Fetch one active project by its URL slug |
| `destiny_promoters_website.api.project_api.get_gallery_projects` | Fetch projects with custom gallery content |
| `destiny_promoters_website.api.gallery.get_gallery_images` | Fetch active general gallery images |
| `destiny_promoters_website.api.gallery_images.get_gallery_projects` | Fetch projects with Gallery Image records |
| `destiny_promoters_website.api.gallery_images.get_project_gallery_tags` | Fetch tags for a project gallery |
| `destiny_promoters_website.api.gallery_images.get_gallery_images` | Fetch project gallery images, optionally filtered by tag |
| `destiny_promoters_website.api.newsletter.subscribe` | Create or check a newsletter subscription |
| `destiny_promoters_website.contact_api.send_suggestion` | Save a contact suggestion and send an email |

These endpoints read and write the app's Frappe DocTypes. Populate and maintain
project and gallery records in the Frappe Desk for content to appear on the
website.

## Configuration notes

- The Vite configuration imports
  `sites/common_site_config.json` from the enclosing bench to determine the
  backend proxy port. Run Vite from the app's `frontend/` directory within a
  normal bench checkout.
- Frappe website route rules for the Vue single-page app are maintained in
  `destiny_promoters_website/hooks.py`. Update those rules when adding new
  frontend paths that need to work on direct browser navigation.
- Configure Frappe's outgoing email account for contact-form email delivery.
  The contact handler's recipient and sender are currently defined in
  `destiny_promoters_website/contact_api.py`; change them there to match the
  deployment's requirements.
- Do not disable CSRF protection on a production site. If local development
  requests fail with a CSRF error, check the Frappe site's development
  configuration and request handling rather than carrying a development-only
  CSRF setting into production.
- Frontend package versions and lockfiles are in `frontend/`. Rebuild assets
  after frontend changes with `npm run build`.

## Troubleshooting

- **Vite cannot start or cannot find `common_site_config.json`:** Run the
  command from `apps/destiny_promoters_website/frontend` inside the bench
  checkout, and verify that the bench has `sites/common_site_config.json`.
- **API requests return 404:** Confirm the app is installed on the site, the
  bench is running, and the request uses the method path listed above. After
  changing Python code, restart the development services if needed.
- **Project pages are empty:** Check that project records exist, are active,
  and contain the fields and child-table records used by the page. Listing
  filters and galleries only show matching records.
- **A route works from the home page but not when refreshed directly:** Check
  that the route is registered in `frontend/src/router.js` and has a matching
  SPA route rule in `destiny_promoters_website/hooks.py`.
- **Contact messages are saved but no email arrives:** Verify the site's
  outgoing Email Account configuration and the recipient/sender settings in
  `destiny_promoters_website/contact_api.py`.
- **Frontend changes do not appear after deployment:** Run `npm run build`
  from `frontend/`, then run `bench build` and restart the site services.

## Contributing

1. Create a branch for your change.
2. Keep frontend changes in `frontend/` and Frappe app changes in
   `destiny_promoters_website/`.
3. Install and run the configured pre-commit checks from the app directory:

   ```bash
   pre-commit install
   pre-commit run --all-files
   ```

4. For frontend changes, run the production build:

   ```bash
   cd frontend
   npm run build
   ```

5. For backend changes, run the relevant app tests on a bench site:

   ```bash
   bench --site your-site run-tests --app destiny_promoters_website
   ```

Open a pull request with a concise description of the change and any relevant
testing performed.

## License

The app declares the MIT license. See [`license.txt`](license.txt). The license
file still contains placeholder copyright year and owner fields; replace them
with the correct details before distributing the project.
