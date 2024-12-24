<template>
<MainLayout title="Search.!">
  <template #rightNav>
      <k-link navbar icon-only>
        <k-icon>
          <SearchFill />
        </k-icon>
      </k-link>
    </template>
    <template #subNav>
        <k-searchbar
        class="mb-2"
          :value="searchQuery"
          disable-button
          disable-button-text="Cancel"
          @clear="handleClear"
          @disable="handleDisable"
          @input="handleSearch"
        >
        </k-searchbar>
    </template>
    <k-list strong inset-material outline-ios>
      <k-list-item v-if="filteredItems.length === 0" title="Nothing found" />
      <k-list-item
        v-for="item in filteredItems"
        :key="item.title"
        :title="item.title"
      />
    </k-list>
</MainLayout>
</template>

<script setup>
 const items = [
    { title: 'FC Ajax' },
    { title: 'FC Arsenal' },
    { title: 'FC Athletic' },
    { title: 'FC Barcelona' },
    { title: 'FC Bayern München' },
    { title: 'FC Bordeaux' },
    { title: 'FC Borussia Dortmund' },
    { title: 'FC Chelsea' },
    { title: 'FC Galatasaray' },
    { title: 'FC Juventus' },
    { title: 'FC Liverpool' },
    { title: 'FC Manchester City' },
    { title: 'FC Manchester United' },
    { title: 'FC Paris Saint-Germain' },
    { title: 'FC Real Madrid' },
    { title: 'FC Tottenham Hotspur' },
    { title: 'FC Valencia' },
    { title: 'FC West Ham United' },
  ];

import { kSearchbar,kList,kListItem } from "konsta/vue";
import { ref, watch } from 'vue';

import MainLayout from "../components/MainLayout.vue";
import SearchFill from "../components/icons/SearchFill.vue";

const searchQuery = ref('');

const handleSearch = (e) => {
  searchQuery.value = e.target.value;
};

const handleClear = () => {
  searchQuery.value = '';
};

const handleDisable = () => {
  console.log('Disable');
};

const filteredItems = ref(items);

watch(searchQuery, () => {
  filteredItems.value = searchQuery.value
    ? items.filter((item) =>
        item.title.toLowerCase().includes(searchQuery.value.toLowerCase())
      )
    : items;
});
</script>