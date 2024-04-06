<script setup>
  import WordleTool from './components/WordleTool.vue'
  import LetterBomb from './components/LetterBomb.vue'
</script>

<template>
  <main>
    <div>
      <WordleTool />
    </div>
    <div>
      <LetterBomb />
    </div>
  </main>
</template>

<style scoped>
  div {
  margin-bottom: 50px;
}
</style>
