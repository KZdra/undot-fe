<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import {
  kCard,
  kIcon,
  kBlock,
  kPreloader,
  kButton,
  kPopup,
  kNavbar,
  kList,
  kListItem,
  kListInput,
} from "konsta/vue";
import CrossFill from "../components/icons/CrossFill.vue";
const isLiked = ref(false);
const popupOpened = ref(false);
const toggleLike = () => {
  isLiked.value = !isLiked.value;
};
import MainLayout from "../components/MainLayout.vue";
import Heart from "../components/icons/post/Heart.vue";
import HeartFill from "../components/icons/post/HeartFill.vue";
import Bubble from "../components/icons/post/Bubble.vue";
import { letdata } from "../master/data.js";
import defaultLogo from "../assets/profileFallback.svg";
const page = ref(1); // Tracks the current page
const isLoading = ref(false); // Tracks loading state
const isLoadingAll = ref(false); // Tracks loading state
const fetchDataPage = async () => {
  if (isLoading.value) return; // Prevent multiple fetches
  isLoading.value = true;
  try {
    // Simulate API request with delay
    await new Promise((resolve) => setTimeout(resolve, 1000)); // Simulate a 1-second delay
    console.log("feteched ke ", page.value);
    page.value += 1; // Increment the page
  } catch (error) {
    console.error("Error fetching data:", error);
  } finally {
    isLoading.value = false;
  }
};
const fetchDataInit = async () => {
  if (isLoadingAll.value) return; // Prevent multiple fetches
  isLoadingAll.value = true;
  try {
    // Simulate API request with delay
    await new Promise((resolve) => setTimeout(resolve, 1000)); // Simulate a 1-second delay
    console.log("feteched ke ", page.value);
    page.value = 1; // Increment the page
  } catch (error) {
    console.error("Error fetching data:", error);
  } finally {
    isLoadingAll.value = false;
  }
};
</script>

<template>
  <MainLayout
    title="Un."
    @doubleClickHome="fetchDataInit()"
    redirectTo="/upload"
  >
    <k-block class="text-center" v-if="isLoadingAll">
      <k-preloader />
    </k-block>
    <k-card
      v-for="item in letdata"
      outline
      header-divider
      footer-divider
      v-if="!isLoadingAll"
    >
      <template #header>
        <div class="flex gap-2 items-center">
          <img
            :src="item.profile_picture_path ?? defaultLogo"
            class="w-7 h-7 rounded-2xl"
          />
          <h1>{{ item.name }}</h1>
        </div>
      </template>
      <img :src="item.post_picture_path" @dblclick="toggleLike()" />
      <template #footer>
        <div>
          <div class="flex gap-2 items-center">
            <span>
              <k-icon @click="toggleLike()">
                <template #material
                  ><HeartFill v-if="isLiked" /><Heart v-else
                /></template> </k-icon
            ></span>
            <span>
              <k-icon @click="() => (popupOpened = true)">
                <template #material> <Bubble /> </template> </k-icon
            ></span>
          </div>
          <!--  -->
          <div>
            <h1 class="font-white font-bold">{{ item.like_count }} likes</h1>
            <p class="font-white">
              <span class="font-bold">{{ item.name }}</span>
              {{ item.content }}
            </p>
            <h1
              class="font-white"
              v-for="komen in JSON.parse(item.recent_comments)"
            >
              <span class="font-bold">{{ komen.user_name }}</span>
              {{ komen.content }}
            </h1>
          </div>
        </div>
      </template>
    </k-card>
    <k-block class="text-center" v-if="!isLoadingAll">
      <k-button clear @click="fetchDataPage()" v-if="!isLoading"
        >Load more</k-button
      >
      <k-preloader v-if="isLoading" />
    </k-block>
    <k-popup
      :opened="popupOpened"
      @backdropclick="() => (popupOpened = false)"
      size="h-screen w-screen overflow-y-auto pb-24"
    >
      <k-navbar title="Comments">
        <template #right>
          <k-link icon-only navbar @click="() => (popupOpened = false)"
            ><k-icon> <CrossFill /> </k-icon
          ></k-link>
        </template>
      </k-navbar>
      <k-list strong-ios outline-ios>
        <k-list-item
          :chevron-material="false"
          link
          title="Yellow Submarine"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Don't Stop Me Now"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-2.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
        <k-list-item
          :chevron-material="false"
          link
          title="Billie Jean"
          text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
        >
          <template #media>
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
            />
          </template>
        </k-list-item>
      </k-list>
      <div class="flex items-center max-w-full">
        <k-list class="w-full">
          <k-list-input outline type="text" placeholder="Comment Here">
          </k-list-input>
        </k-list>
        <div class="mr-2">
          <button
            class="flex items-center bg-blue-500 text-white gap-1 px-4 py-2 cursor-pointer font-semibold tracking-widest rounded-md hover:bg-blue-400 duration-300 hover:gap-2 hover:translate-x-3"
          >
            Send
            <svg
              class="w-5 h-5"
              stroke="currentColor"
              stroke-width="1.5"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5"
                stroke-linejoin="round"
                stroke-linecap="round"
              ></path>
            </svg>
          </button>
        </div>
      </div>
    </k-popup>
  </MainLayout>
</template>
