<template>
    <div class="font">

        <!-- HERO SECTION -->
        <!-- First Section -->
        <div class="relative w-full h-auto mb-6">
            <!-- Background Image -->
            <img :src="aboutData.heroImage" alt="About Us Image" class="w-full h-auto object-cover" />

            <!-- Overlapping Button -->
            <router-link to="contact-us"><button class="absolute top-[78%] right-[8%] bg-[#1a1a1a] text-white px-6 py-2 rounded-md flex items-center text-xs space-x-2 hover:bg-gray-800 transition duration-300
                 sm:text-xs sm:px-5 sm:py-[10px] 
                 xs:text-[10px] xs:px-4 xs:py-2">
                    <span>Contact</span>
                    <span v-if="aboutData.buttonIcon">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="w-4 h-3">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="M13.5 4.5 21 12m0 0-7.5 7.5M21 12H3" />
                        </svg>
                    </span>
                </button>
            </router-link>
        </div>

        <!-- ABOUT INTRO -->
        <div class="container mb-16">
            <div class="row align-items-center">

                <!-- TEXT -->
                <div class="col-md-8">
                    <div class="text-[#E7C873] text-7xl font-semibold mb-2">
                        About Us
                    </div>

                    <div class="text-4xl font-bold mb-4">
                        Destiny Developers & Promoters, Bangalore
                    </div>

                    <p class="text-gray-700 mb-3">
                        Destiny Developers & Promoters is a dynamic real estate solutions company based in Bangalore,
                        specializing in Sales, Marketing, Construction, and Interior Design.
                    </p>

                    <p class="text-gray-700">
                        We are dedicated to delivering end-to-end property solutions that combine
                        innovation, quality, and strategic execution. With deep market knowledge and a
                        customer-first approach, we help clients turn their real estate goals into
                        reality — whether it's buying, selling, building, or designing their dream space.
                    </p>

                    <p class="text-gray-700">
                        We are a creative interior design company dedicated to transforming spaces into inspiring,
                        functional, and comfortable environments with a perfect balance of aesthetics and practicality.
                        Our team believes every space tells a story, and we bring it to life through thoughtful
                        planning, innovative design, and high-quality execution.
                    </p>
                </div>

                <!-- IMAGE -->
                <div class="col-md-4 text-center">
                    <img :src="aboutData.aboutImage" class="rounded-5 shadow img-fluid" />
                </div>

            </div>
        </div>

        <!-- CORE SERVICES -->
        <div class="bg-gray-100 py-16 mb-16">
            <div class="container">

                <div class="text-center mb-4">
                    <div class="text-[#E7C873] font-semibold text-7xl">Our Core Services</div>
                </div>

                <div class="row g-4">

                    <div class="col-md-4">
                        <div class="bg-white p-4 rounded-4 shadow h-full">
                            <div class="text-2xl font-semibold mb-3">
                                Sales & Marketing
                            </div>
                            <p class="text-sm text-gray-600">
                                Strategic real estate sales and marketing solutions for residential
                                and commercial projects including branding, lead generation,
                                and deal closure.
                            </p>
                        </div>
                    </div>

                    <div class="col-md-4">
                        <div class="bg-white p-4 rounded-4 shadow h-full">
                            <div class="text-2xl font-semibold mb-3">
                                Construction
                            </div>
                            <p class="text-sm text-gray-600">
                                Residential and commercial construction with a focus on
                                quality craftsmanship, timely delivery, and cost efficiency.
                            </p>
                        </div>
                    </div>

                    <div class="col-md-4">
                        <div class="bg-white p-4 rounded-4 shadow h-full">
                            <div class="text-2xl font-semibold mb-3">
                                Interior Design
                            </div>
                            <p class="text-sm text-gray-600">
                                Functional and aesthetic interior spaces designed with
                                creativity, comfort, and elegance tailored to client needs.
                            </p>
                        </div>
                    </div>

                </div>
            </div>
        </div>

        <!-- VISION & MISSION -->
        <div class="container mb-16">
            <div class="row">

                <div class="col-md-6">
                    <div class="bg-[#1a1a1a] text-white p-5 rounded-4 h-full">
                        <div class="text-3xl font-bold mb-3">
                            Our Vision
                        </div>

                        <p>
                            Our vision is to redefine the way people. experience their living and working spaces. We
                            strive to create interiors that are not only visually stunning but also comfortable,
                            functional, and timeless. By blending creativity, innovation, and sustainability, we aim to
                            design spaces that reflect individuality and elevate everyday living. Our goal is to become
                            a trusted name in interior design, setting new standards of excellence and inspiring
                            lifestyles through every project we deliver.
                        </p>
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="bg-gray-100 p-5 rounded-4 h-full">
                        <div class="text-3xl font-bold mb-3">
                            Our Mission
                        </div>

                        <p>Our mission is to deliver exceptional interior design solutions that blend creativity,
                            comfort, and functionality. We are committed to understanding our clients' needs and
                            transforming their ideas into spaces that truly reflect their lifestyle and vision. Through
                            innovative design, attention to detail, and quality execution, we aim to create environments
                            that inspire and endure. Our focus is on building long-term relationships by ensuring
                            satisfaction, trust, and excellence in every project</p>
                    </div>
                </div>

            </div>
        </div>

        <!-- CTA SECTION -->
        <div class="container mb-20">
            <div class="bg-gray-100 rounded-4 p-5 text-center">

                <div class="text-3xl font-bold mb-3">
                    Building More Than Properties
                </div>

                <p class="mb-4 text-gray-700">
                    At Destiny Developers & Promoters, we believe in more than just building properties —
                    we build trust, value, and lasting partnerships.
                </p>

                <router-link to="/listing">
                    <button class="bg-[#1a1a1a] text-white px-5 py-2 text-sm rounded-lg hover:bg-black">
                        View Projects →
                    </button>
                </router-link>

            </div>
        </div>

    </div>
</template>

<script setup>
const aboutData = {
    heroImage: new URL('../assets/images/AboutUs/AboutUs.png', import.meta.url).href,
    aboutImage: new URL('../assets/images/AboutUs/About_2.png', import.meta.url).href
};
</script>
