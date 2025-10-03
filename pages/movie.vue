<template>
  <div>
    <!-- topics_id=57 -->
<div v-if="response?.details">
  <h2>{{ response?.details?.ext_1 }}</h2>
  <div v-html="response?.details?.ext_2"></div>
</div>

<!-- topics_id=56 -->
<div v-if="response3?.details" style="margin-top:40px">
  <h2>{{ response3?.details?.ext_1 }}</h2>
  <div v-html="response3?.details?.ext_2"></div>
</div>

<!-- topics_id=58 -->
<div v-if="response2?.details" style="margin-top:40px">
  <h2>{{ response2?.details?.ext_1 }}</h2>
  <div v-html="response2?.details?.ext_2"></div>
</div>

    <pre v-if="error" style="padding:8px;background:#f5f5f5">{{ error }}</pre>
    <div v-else-if="loading">loading...</div>
  </div>
</template>

<script setup lang="ts">
const { data: response, error: error1, pending: p1 } = await useFetch(
  'https://nizumi3.g.kuroco.app/rcms-api/1/content/details/57',
  { key: 'details-57' } // キャッシュキーを明示
)

const { data: response3, error: error3, pending: p2 } = await useFetch(
  'https://nizumi3.g.kuroco.app/rcms-api/1/content/details/56',
  { key: 'details-56' }
)

const { data: response2, error: error2, pending: p3 } = await useFetch(
  'https://nizumi3.g.kuroco.app/rcms-api/1/content/details/58',
  { key: 'details-58' }
)

// どれかにエラーがあれば表示
const error = computed(() => error1.value || error2.value || error3.value || null)

// 読み込み中フラグ
const loading = computed(() => p1.value || p2.value || p3.value)
</script>
