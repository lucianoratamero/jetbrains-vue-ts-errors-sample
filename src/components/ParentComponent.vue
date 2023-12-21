<script setup lang="ts">
import WelcomeItem from './ChildComponentWithErrors.vue'
</script>

<template>
  <WelcomeItem/>
  <WelcomeItem :data="{ obj1: { obj2: 'obj2' }}"/>
</template>
