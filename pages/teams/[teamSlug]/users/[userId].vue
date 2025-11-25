<template>
  <div>
    {{ $route.params.userId }}
    {{ $route.params.teamSlug }}
    {{ $route.params }}
  </div>
</template>
<script setup>
const route=  useRoute();

onMounted(() =>{
  console.log(route, "iffi");
  
})
</script>