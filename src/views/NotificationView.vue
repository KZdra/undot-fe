<script setup>
import MainLayout from "../components/MainLayout.vue";
import { kList, kListItem } from "konsta/vue";
import HeartFill from "../components/icons/HeartFill.vue";
</script>

<template>
  <MainLayout title="Notifications.">
    <template #rightNav>
      <k-link navbar icon-only>
        <k-icon>
          <HeartFill />
        </k-icon>
      </k-link>
    </template>
    <k-list strong-ios outline-ios>
      <!--  -->
      <k-list-item
        :chevron-material="false"
        link
        title="Yellow Submarine"
        after="12s"
        text="Has Like Your Post!"
      >
        <template #media>
          <img
            class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
            src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
            width="80"
            alt="demo"
          />
        </template>
      </k-list-item>
      <k-list-item
        :chevron-material="false"
        link
        title="Yellow Submarine"
        after="12s"
        text="Has Like Your Post!"
      >
        <template #media>
          <img
            class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
            src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
            width="80"
            alt="demo"
          />
        </template>
      </k-list-item>
      <k-list-item
        :chevron-material="false"
        link
        title="Yellow Submarine"
        after="12s"
        text="Has Like Your Post!"
      >
        <template #media>
          <img
            class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
            src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
            width="80"
            alt="demo"
          />
        </template>
      </k-list-item>
    </k-list>
  </MainLayout>
</template>
