<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem :game-status="gameStatus" v-for="field in fields" :field="field" :key="'item-' + field.id"
        @selectField="selectField($event)"/>
    </div>
    
    <p class="difficult">Сложность: <strong>{{ difficult }}</strong></p>
    <p class="win" v-if="isWin">Поздравляем! Продолжаем играть!</p>
    <p class="fail" v-if="isFail">Вы проиграли. Попробуйте еще раз!</p>
  
    <button class="btn" @click="start" :disabled="!canStartGame">Старт</button>
  </div>
</template>

<script>
import BoardItem from './BoardItem.vue';
import useGameInit from "@/components/composables/useGameInit";
import useGameStart from "@/components/composables/useGameStart";
import useGameProcess from "@/components/composables/useGameProcess";
import { GAME_STATUS } from "@/constants";
import { ref } from 'vue';

export default {
  name: 'Board',
  props: {},
  components: {
    BoardItem,
  },
  setup() {
    const number = 25;
    const gameStatus = ref(GAME_STATUS.NONE);
    
    const { difficult, fields, init } = useGameInit(number);
    
    const { start, canStartGame } = useGameStart(init, fields, difficult, number, gameStatus);

    const { selectField, isWin, isFail } = useGameProcess(fields, gameStatus, difficult, start);
    
    return {
      number,
      difficult,
      fields,
      init,
      start,
      gameStatus,
      canStartGame,
      selectField,
      isWin,
      isFail
    }
  },
}
</script>

<style scoped>
.board-wrapper {
  margin-bottom: 100px;
}

.board {
  display: grid;
  flex-wrap: wrap;
  width: 400px;
  height: 400px;
  
  grid-template-columns: repeat(5, 1fr);

  gap: 10px;
 
  background: #eee;
  margin: 0 auto;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
  /* Глубокая тень для доски */
}

.board-item {
  width: 50px;
  height: 50px;
  background: #ffffff;
  border-radius: 8px;
  box-shadow:
    0 12px 18px rgba(0, 0, 0, 0.3),
    /* Внешняя глубокая тень */
    inset 0 6px 9px rgba(255, 255, 255, 0.8);
  /* Глубокая внутренняя тень */
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s, box-shadow 0.3s;
  /* Более плавный эффект */
}

.board-item:hover {
  transform: translateY(-6px);
  /* Увеличенный сдвиг вверх */
  box-shadow:
    0 16px 24px rgba(0, 0, 0, 0.35),
    /* Увеличенная внешняя тень при наведении */
    inset 0 8px 12px rgba(255, 255, 255, 0.7);
  /* Увеличенная внутренняя тень */
}

.board-item:active {
  transform: translateY(0);
  box-shadow:
    0 10px 15px rgba(0, 0, 0, 0.4),
    /* Уменьшенная внешняя тень при нажатии */
    inset 0 4px 6px rgba(255, 255, 255, 0.6);
  /* Вдавленная внутренняя тень */
}

.difficult {
  text-align: center;
  margin-bottom: 20px;
}

.btn {
  background: #42b983cc;
  color: white;
  border: none;
  border-radius: 2px;
  padding: 10px 30px;
  margin: 10px 0;
  cursor: pointer;
  outline: none;
}

button:hover {
  background: #42b983;
}

button:disabled {
  opacity: 0.5;
}

.win {
  color: #42b983;
}

.fail {
  color: #ff000055;
}
</style>
