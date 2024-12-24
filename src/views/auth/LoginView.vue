<script setup>
import {
  kPage,
  kBlock,
  kLink,
  kIcon,
  kList,
  kListInput,
  kButton,
  kListButton,
} from "konsta/vue";
</script>
<template>
  <k-page>
    <k-block>
      <h1 class="text-center font-bold text-4xl">Login</h1>
      <k-list>
        <k-list-input
          outline
          label="E-mail"
          floating-label
          type="email"
          placeholder="e-mail"
        >
          <template #media>
            <demo-icon />
          </template>
        </k-list-input>

        <k-list-input
          outline
          label="Password"
          floating-label
          type="password"
          placeholder="password"
        >
          <template #media>
            <demo-icon />
          </template>
        </k-list-input>
        <k-list-button>
          <k-button large>Login</k-button>
        </k-list-button>
        <div class="text-center mt-2">
          no account? no problem
          <k-link :link-props="{ to: '/register' }" component="router-link">
            Register Here
          </k-link>
        </div>
      </k-list>
    </k-block>
  </k-page>
</template>
