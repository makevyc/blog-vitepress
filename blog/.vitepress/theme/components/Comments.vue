<template>
  <div id="gitalk-container"></div>
</template>
<script lang="ts" setup>
import "gitalk/dist/gitalk.css";
import Gitalk from "gitalk";
import { onMounted } from "vue";
import { useData } from "vitepress";

const { theme, page } = useData();

const lang = location.href.includes('/zh/') ? 'zh-CN' : 'en';

// Generate a unique ID for each page
const generateId = () => {
  const path = location.pathname;
  // Remove leading slash and trailing slash
  const cleanPath = path.replace(/^\/|\/$/g, '');
  // Use the full path as ID, but limit to 50 characters
  return cleanPath.length > 50 ? cleanPath.substring(0, 50) : cleanPath;
};

const gitalk = new Gitalk({
  ...theme.value.gitalk,
  id: generateId(),
  title: page.value.title,
  language: lang,
  distractionFreeMode: false,
  createIssueManually: false,
});

onMounted(() => {
  gitalk.render("gitalk-container");
});
</script>
<style scoped>

</style>
