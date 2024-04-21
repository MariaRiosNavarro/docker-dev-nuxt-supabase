import About from './about.vue';
<script setup>
import { ref, onMounted, provide } from "vue";
// import { createClient } from "@supabase/supabase-js";
import { supabase } from "../utils/supabase.js";

const homeSection = ref([]);

const getHomeData = async () => {
  try {
    const { data, error } = await supabase.from("home_section1").select();
    if (error) {
      throw error;
    }
    homeSection.value = data;
    console.log(data);
  } catch (error) {
    console.error("Error fetching todos:", error.message);
    console.log(error);
  }
};

onMounted(() => {
  getHomeData();
});

provide("supabaseClient", supabase);
</script>

<template>
  <section
    class="h-screen w-screen flex flex-col justify-center items-center bg-green-100 gap-4"
  >
    <article
      v-for="(section, index) in homeSection"
      :key="section.id"
      :class="`bg-cover bg-center bg-no-repeat w-full p-8 relative`"
      :style="{ 'background-image': `url('${section.image}')` }"
    >
      <div
        class="flex flex-col items-center gap-4 backdrop-blur-sm rounded-md p-8 shadow-black"
      >
        <h2
          class="text-3xl font-bold mix-blend-multiply bg-white rounded text-center px-3 py-1"
        >
          {{ section.title }}
        </h2>
        <p class="text-lg mix-blend-multiply text-center">
          {{ section.subtitle }}
        </p>
        <a
          :href="section.input_link"
          class="bg-blue-500 text-white hover:underline rounded w-fit px-3 py-1"
          >{{ section.input_text }}</a
        >
        <p class="mix-blend-multiply font-bold">{{ section.description }}</p>
      </div>
    </article>
  </section>
</template>
