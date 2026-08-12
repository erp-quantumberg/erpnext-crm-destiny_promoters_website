<template>
    <div
        v-if="amenities.length"
        class="container mx-auto px-4 py-8"
    >
        <!-- Section Heading -->
        <div class="text-center mb-8">
            <div class="font-semibold text-7xl">
                Building Amenities
            </div>
        </div>

        <!-- Amenities Grid -->
        <div class="grid grid-cols-2 md:grid-cols-6 gap-6">

            <div
                v-for="(amenitie, index) in amenities"
                :key="amenitie.name || index"
                class="bg-white rounded-xl shadow p-4 flex flex-col items-center text-center"
            >

                <!-- Amenity Image -->
                <img
                    v-if="amenitie.image"
                    :src="amenitie.image"
                    :alt="amenitie.amenity_name"
                    class="w-16 h-16 object-contain"
                />

                <!-- Amenity Name -->
                <p class="mt-2 text-sm font-bold">
                    {{ amenitie.amenity_name }}
                </p>

            </div>

        </div>
    </div>
</template>

<script setup>

defineProps({
    amenities: {
        type: Array,
        default: () => []
    }
})

</script>