<script setup lang="ts">
const loading = ref(false);
const selected = ref();

async function search(search: string) {
  loading.value = true;

  const users = await $fetch<any[]>("/api/city", {
    params: { search },
  });

  loading.value = false;

  return users.results;
}
</script>

<template>
  <UCard>
    <template #header>
      {{ selected }}

    </template>
    <UInputMenu
      v-model="selected"
      :search="search"
      :loading="loading"
      placeholder="Search for a user..."
      option-attribute="name"
      trailing
      by="id"
      value-attribute='id'
      :debounce="600"
    />
  </UCard>
</template>
