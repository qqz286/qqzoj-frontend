<template>
  <div id="app">
    <BasicLayout></BasicLayout>
  </div>
</template>

<style></style>
<script setup lang="ts">
import BasicLayout from "@/layout/BasicLayout.vue";
import { useRouter } from "vue-router";
import { useStore } from "vuex";

const router = useRouter();
const store = useStore();
router.beforeEach((to, from, next) => {
  if (to.meta.access === "canAdmin") {
    if (store.state.loginUser?.role !== "admin") {
      next("/noAuth");
      return;
    }
  }
  next();
});
</script>