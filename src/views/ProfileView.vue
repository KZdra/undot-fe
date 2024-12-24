<template>
    <MainLayout :title="user.informations.username">
        <!-- Start OF profile Setions -->
      <k-block>
        <div class="flex items-center justify-between mr-4">
          <img :src="user.informations.profile_picture_path ?? FallbackProfile" class="w-24 h-24 rounded-full" />
          <div class="text-center text-base">
            <h2 class="font-bold">{{user.posts}}</h2>
            <h1>posts</h1>
          </div>
          <div class="text-center text-base">
            <h2 class="font-bold">{{user.followers}}</h2>
            <h1>followers</h1>
          </div>
          <div class="text-center text-base">
            <h2 class="font-bold">{{user.followings}}</h2>
            <h1>following</h1>
          </div>
        </div>
        <div class="mt-2 ml-2">
            <h2 class="font-bold font-2xl">{{user.informations.name}}</h2>
            <h2 class="font-base">{{user.informations.bio ?? ''}}</h2>
        </div>
        <div class="flex justify-center items-center mt-3 w-100">
          <button 
            class="bg-blue-500 text-white px-4 py-2 w-full rounded-2xl hover:bg-blue-600"
          >
            Edit Profile
          </button>
        </div>
      </k-block>
      <!-- END OF PROFILE SECTIONS -->
    </MainLayout>
  </template>
  
  <script setup>
  import MainLayout from "../components/MainLayout.vue";
  import { kBlock } from "konsta/vue";
  import { user } from "../master/profile";
  import FallbackProfile from "../assets/profileFallback.svg"
  </script>
  