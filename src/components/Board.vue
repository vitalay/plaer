<template>
  <div class="board-wrapper">
    <div class="board">
      <borderItem v-for="i in 25" :key="'item-' + i" />
    </div>

    <p class="difficult"><strong>Сложность: {{ difficult }}</strong></p>
    <button class="btn">Новая игра</button>
  </div>
</template>

<script>
import { ref } from 'vue'
import BorderItem from './BorderItem.vue'

export default {
  name: 'Board',
  props: {},
  components: {
    BorderItem,
  },
  setup() {

    const difficult = ref(5);

    return {
      difficult
    }
  }
}
</script>


<style scoped>
.board-wrapper {
  margin-bottom: 100px;
}

.board {
  width: 300px;
  background: #eee;
  margin: 0, auto;
}

.difficult {
  text-align: center;
  margin-bottom: 20px;
}

.btn {
  display: block;
  margin: 0 auto;
  padding: 10px 20px;
  border: none;
  background: #0eddcf;
  color: #0914ec;
  cursor: pointer;
  font-size: 16px;
}
</style>
