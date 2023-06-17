<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import { useForm } from "@inertiajs/vue3";

const props = defineProps({
    item: {
        type: Object,
        default: null,
    },
});

const form = useForm({
    name: props.item ? props.item.name : null,
    description: props.item ? props.item.description : null,
});

function submit() {
    props.item
        ? form.put("/item/" + props.item.id)
        : form.post("/item/");
}
</script>


<template>
    <AppLayout title="Dashboard">
      <template #header>
        <h2 class="font-semibold text-xl text-gray-800 leading-tight">
          Items
        </h2>
      </template>

      <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
          <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
            <form class="p-8">
              <div class="mb-4">
                <label for="name" class="block text-gray-700 font-bold mb-2">Name:</label>
                <input type="text" id="name" v-model="form.name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-indigo-500" />
                <div v-if="form.errors.name" class="text-red-500 mt-2">{{ form.errors.name }}</div>
              </div>

              <div class="mb-4">
                <label for="description" class="block text-gray-700 font-bold mb-2">Description:</label>
                <textarea id="description" v-model="form.description" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-indigo-500"></textarea>
                <div v-if="form.errors.description" class="text-red-500 mt-2">{{ form.errors.description }}</div>
              </div>

              <div class="flex justify-end">
                <button @click="submit()" :disabled="form.processing" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                  {{ item ? "Update" : "Create" }}
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </AppLayout>
  </template>
