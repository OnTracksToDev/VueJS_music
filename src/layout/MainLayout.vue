<script setup>
import { records } from "@/data/allRecords";
import CardRecord from "@/components/CardRecord.vue";
import FilterRecord from "@/components/FilterRecord.vue";
import { ref } from "vue";

const filteredRecords = ref(records);

const applyFilters = (filteredData) => {
  filteredRecords.value = filteredData;
};
</script>

<template>
  <filter-record @filters-applied="applyFilters"></filter-record>

  <main class="bg-white py-5 ml-6 basis-auto">
    <section class="text-gray-600 body-font">
      <div v-if="filteredRecords.length > 0" v-for="record in filteredRecords" :key="record.id">
        <card-record :record="record"></card-record>
      </div>
      <div v-else>
        <p>No records match the current filters.</p>
      </div>
    </section>
  </main>
</template>
