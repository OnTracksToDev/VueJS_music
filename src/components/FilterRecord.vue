<script setup>
import { ref, defineProps, defineEmits } from "vue";

import { records } from "@/data/allRecords";

const props = defineProps(["filteredRecords"]);
const emit = defineEmits();

const filters = ref({
  inStock: false,
});

const sortBy = ref("Year");

const filteredRecords = ref(records);

const applyFilters = () => {
  const filteredData = records.filter((item) => {
    // Filtrer stock
    if (filters.value.inStock && item.stock === 0) {
      return false; 
    }

    // Filtrer  tri Year 
    if (sortBy.value === "Year" && !item.year) {
      return false; 
    }

    //Filtrer  tri Pitchfork
    if (sortBy.value === "Pitchfork" && !item.pitchforkPos) {
      return false; 
    }

    return true; // Garde éléments qui passent tous les filtres
  });
  if (sortBy.value === "Year") {
    filteredData.sort((a, b) => b.year - a.year);
  }

if (sortBy.value === 'Pitchfork') {
  filteredData.sort((a, b) => (a.pitchforkPos) - (b.pitchforkPos));
}
  console.log("Filtered data:", filteredRecords.value); // Émettre l'événement avec les données filtrées
  emit("filters-applied", filteredData);
};
</script>

<template>
  <div class="px-8 bg-cyan-100">
    <div class="mt-2 basis-1/4">
      <div class="overflow-hidden shadow sm:rounded-md">
        <div class="bg-white p-6 w-64 h-96">
          <fieldset>
            <legend class="sr-only">Filtres</legend>
            <div class="text-base font-medium text-gray-900" aria-hidden="true">
              Filtres
            </div>
            <div class="mt-4 space-y-4">
              <div class="flex items-start">
                <div class="flex h-5 items-center">
                  <input
                    id="inStock"
                    name="inStock"
                    type="checkbox"
                    class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                    v-model="filters.inStock"
                    @change="applyFilters"
                  />
                </div>
                <div class="ml-3 text-sm">
                  <label for="inStock" class="font-medium text-cyan-700"
                    >In stock only</label
                  >
                </div>
              </div>
            </div>
            <label
              for="sortBy"
              class="block text-sm mt-2 font-medium text-cyan-700"
              >Sort by</label
            >
            <select
              id="sortBy"
              name="sortBy"
              autocomplete="country-name"
              class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
              v-model="sortBy"
              @change="applyFilters"
            >
              <option>Year</option>
              <option>Pitchfork</option>
            </select>
          </fieldset>
        </div>
      </div>
    </div>
  </div>
</template>
