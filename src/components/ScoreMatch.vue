<template>
    <div class="score-match">
      <h2>分数匹配结果</h2>
      <p v-if="matchResult.success">
        你的分数：{{ matchResult.data.score }}
        <br>
        匹配院校：{{ matchResult.data.matchedSchools.join('、') }}
      </p >
      <p v-else>数据加载失败，请稍后再试</p >
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const matchResult = ref({});
  
  const fetchMatchData = async () => {
    // 替换为你自己的Worker域名
    const workerUrl = "https://gaokao-volunteer-api.tsu452717.workers.dev/";
    const res = await fetch(workerUrl);
    matchResult.value = await res.json();
  };
  
  onMounted(() => {
    fetchMatchData();
  });
  </script>
  
  <style scoped>
  .score-match {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
  }
  </style>