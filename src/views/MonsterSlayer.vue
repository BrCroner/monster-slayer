<template>
  <div class="container mt-5">
    <div id="game">
      <section id="monster" class="container">
        <h2>Vida do Monstro</h2>
        <div class="healthbar">
          <div class="healthbar__value" :style="monsterBarStyles"></div>
        </div>
      </section>
      <section id="player" class="container">
        <h2>Sua Vida</h2>
        <div class="healthbar">
          <div class="healthbar__value" :style="playerBarStyles"></div>
        </div>
      </section>
      <section class="info" v-if="winner">
        <h2>GAME OVER!</h2>
        <h3 v-if="winner === 'monster'">Você perdeu!</h3>
        <h3 v-else-if="winner === 'player'">Você ganhou!</h3>
        <h3 v-else>empate!</h3>
        <button @click="startGame">NOVO JOGO</button>
      </section>
      <section id="controls" v-else>
        <button @click="attackMonster">ATAQUE</button>
        <button :disabled="canUseSpecialAttack" @click="specialAttackMonster">
          ATAQUE ESPECIAL
        </button>
        <button @click="healPlayer">CURA</button>
        <button @click="surrender">SE RENDER</button>
      </section>
      <section id="log" v-if="logMessages.length" class="container">
        <h2>Log de Batalha</h2>
        <ul>
          <li v-for="(logMessage, index) in logMessages" :key="index">
            <span
              :class="{
                'log--player': logMessage.actionBy === 'player',
                'log--monster': logMessage.actionBy === 'monster',
              }"
              >{{
                logMessage.actionBy === 'player' ? 'Player' : 'Monstro'
              }}</span
            >
            <span v-if="logMessage.actionType === 'heal'"
              >se curou com
              <span class="log--heal">{{ logMessage.actionValue }}</span>
            </span>
            <span v-else>
              atacou e causou
              <span class="log--damage">{{ logMessage.actionValue }}</span> de
              dano.
            </span>
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>
<script>
function randomNumber(min, max) {
  return Math.floor(Math.random() * (max - min)) + min;
}
export default {
  data() {
    return {
      playerHealth: 100,
      monsterHealth: 100,
      currentRound: 0,
      winner: null,
      logMessages: [],
    };
  },
  computed: {
    monsterBarStyles() {
      if (this.monsterHealth < 0) {
        return { width: '0%' };
      }
      return { width: this.monsterHealth + '%' };
    },
    playerBarStyles() {
      if (this.playerHealth < 0) {
        return { width: '0%' };
      }
      return { width: this.playerHealth + '%' };
    },
    canUseSpecialAttack() {
      return this.currentRound % 3 !== 0;
    },
  },
  watch: {
    playerHealth(value) {
      if (value <= 0 && this.monsterHealth <= 0) {
        this.winner = 'draw'; //empate
      } else if (value <= 0) {
        this.winner = 'monster'; //derrota
      }
    },
    monsterHealth(value) {
      if (value <= 0 && this.playerHealth <= 0) {
        this.winner = 'draw'; //empate
      } else if (value <= 0) {
        this.winner = 'player'; //vitória
      }
    },
  },
  methods: {
    startGame() {
      this.playerHealth = 100;
      this.monsterHealth = 100;
      this.winner = null;
      this.currentRound = 0;
      this.logMessages = [];
    },
    attackMonster() {
      this.currentRound++;
      const attackValue = randomNumber(5, 12);
      this.monsterHealth -= attackValue;
      this.addLogMessage('player', 'attack', attackValue);
      this.attackPlayer();
    },
    attackPlayer() {
      const attackValue = randomNumber(8, 15);
      this.playerHealth -= attackValue;
      this.addLogMessage('monster', 'attack', attackValue);
    },
    specialAttackMonster() {
      this.currentRound++;
      const attackValue = randomNumber(10, 25);
      this.monsterHealth -= attackValue;
      this.addLogMessage('player', 'attack', attackValue);
      this.attackPlayer();
    },
    healPlayer() {
      this.currentRound++;
      const healValue = randomNumber(8, 20);
      if (this.playerHealth + healValue > 100) {
        this.playerHealth = 100;
      } else {
        this.playerHealth += healValue;
      }
      this.addLogMessage('player', 'heal', healValue);
      this.attackPlayer();
    },
    surrender() {
      this.winner = 'monster';
    },
    addLogMessage(who, what, value) {
      this.logMessages.unshift({
        actionBy: who,
        actionType: what,
        actionValue: value,
      });
    },
  },
};
</script>
<style scoped>
section {
  width: 90%;
  max-width: 40rem;
  margin: auto;
}

.healthbar {
  width: 100%;
  height: 40px;
  border: 1px solid #575757;
  margin: 1rem 0;
  background: #fde5e5;
  border-radius: 5px;
}

.healthbar__value {
  background-color: #00a876;
  width: 100%;
  height: 100%;
  border-radius: 5px;
}

.container {
  text-align: center;
}

#monster h2,
#player h2 {
  margin: 0.25rem;
}

#controls {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

button {
  font: inherit;
  border: 1px solid #88005b;
  background-color: #88005b;
  color: white;
  padding: 1rem 2rem;
  border-radius: 5px;
  margin: 1rem;
  width: 20rem;
  cursor: pointer;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

button:focus {
  outline: none;
}

button:hover,
button:active {
  background-color: #af0a78;
  border-color: #af0a78;
  box-shadow: 1px 1px 8px rgba(0, 0, 0, 0.26);
}

button:disabled {
  background-color: #ccc;
  border-color: #ccc;
  box-shadow: none;
  color: #3f3f3f;
  cursor: not-allowed;
}

#log ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

#log li {
  margin: 0.5rem 0;
}

.log--player {
  color: #7700ff;
}

.log--monster {
  color: #da8d00;
}

.log--damage {
  color: red;
}

.log--heal {
  color: green;
}
</style>
