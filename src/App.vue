<script setup>
import HeaderLayout from "@/layout/HeaderLayout.vue";
import MainLayout from "@/layout/MainLayout.vue";
import FooterLayout from "@/layout/FooterLayout.vue";
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <header-layout></header-layout>

    <div class="flex flex-row">
      <main-layout></main-layout>
    </div>
    <footer-layout></footer-layout>
  </div>
</template>
