<script setup>
import { RouterView } from 'vue-router'
import { kApp} from 'konsta/vue';
</script>

<template>
   
   <k-app theme="material" safe-areas  :touchRipple="true">
      <router-view>
  </router-view>
   </k-app>
</template>
