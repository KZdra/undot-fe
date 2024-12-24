<script setup>
import { kPage, kNavbar, kLink, kIcon, kTabbar, kTabbarLink } from "konsta/vue";
import HeartFill from "./icons/HeartFill.vue";
import HomeFill from "./icons/HomeFill.vue";
import SearchFill from "./icons/SearchFill.vue";
import PlusFill from "./icons/PlusFill.vue";
import PersonCircleFill from "./icons/PersonCircleFill.vue";
import { useRoute } from "vue-router";
const route = useRoute();
defineProps({
  title: String,
  notifBadge: Number,
  redirectTo: String,
});
</script>

<template>
  <k-page>
    <k-navbar :title="title">
      <template #right>
        <k-link
          navbar
          icon-only
          :link-props="{ to: redirectTo ?? '' }"
          component="router-link"
        >
          <k-icon>
            <slot name="rightNav">
              <PlusFill v-if="route.name !== 'profile'" />
            </slot>
          </k-icon>
        </k-link>
      </template>
      <template #subnavbar v-if="$slots.subNav">
        <slot name="subNav"></slot>
      </template>
    </k-navbar>
    <div class="pb-20">
      <slot> </slot>
    </div>
  </k-page>
  <k-tabbar :labels="false" :icons="true" class="left-0 bottom-0 fixed">
    <k-tabbar-link
      :link-props="{ to: '/' }"
      component="router-link"
      @dblclick="$emit('doubleClickHome')"
      :active="route.name == 'home'"
    >
      <template #icon>
        <k-icon> <HomeFill /></k-icon>
      </template>
    </k-tabbar-link>
    <k-tabbar-link
      :link-props="{ to: '/search' }"
      component="router-link"
      :active="route.name == 'search'"
    >
      <template #icon>
        <k-icon> <SearchFill /> </k-icon>
      </template>
    </k-tabbar-link>
    <k-tabbar-link
      :link-props="{ to: '/notifications' }"
      component="router-link"
      :active="route.name == 'notifications'"
    >
      <template #icon>
        <k-icon :badge="notifBadge" :badge-colors="{ bg: 'bg-red-500' }">
          <HeartFill
        /></k-icon>
      </template>
    </k-tabbar-link>
    <k-tabbar-link
      :link-props="{ to: '/profile' }"
      component="router-link"
      :active="route.name == 'profile'"
    >
      <template #icon>
        <!-- IF Profile Picture is not null -->
        <!-- <img src="../assets/logo.svg" class="w-6 h-6"> -->
        <!-- IF Profile Pictures is NULL -->
        <k-icon> <PersonCircleFill /> </k-icon>
      </template>
    </k-tabbar-link>
  </k-tabbar>
</template>
