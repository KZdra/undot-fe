<script setup>
import {
  kPage,
  kBlock,
  kLink,
  kList,
  kListInput,
  kButton,
  kListButton,
} from "konsta/vue";
</script>
<template>
  <k-page>
    <k-block>
      <h1 class="text-center font-bold text-4xl">Register</h1>
      <k-list>
        <k-list-input
          outline
          label="Username"
          floating-label
          type="text"
          placeholder="Username"
        >
          <template #media>
            <demo-icon />
          </template>
        </k-list-input>
        <k-list-input
          outline
          label="Name"
          floating-label
          type="text"
          placeholder="Name"
        >
          <template #media>
            <demo-icon />
          </template>
        </k-list-input>
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
          placeholder="Password"
        >
          <template #media>
            <demo-icon />
          </template>
        </k-list-input>

        <k-list-input
          outline
          label="Confirm Password"
          floating-label
          type="password"
          placeholder="Confirm password"
        >
          <template #media>
            <demo-icon />
          </template>
        </k-list-input>
        <k-list-button>
          <k-button large>Register</k-button>
        </k-list-button>
        <div class="text-center mt-2">
          Have an account?
          <k-link :link-props="{ to: '/login' }" component="router-link">
            Login Here
          </k-link>
        </div>
      </k-list>
    </k-block>
  </k-page>
</template>
