<script setup>
import { ref } from 'vue'
import DefendMechanism from './components/Defend-Mechanism.vue'
import AttackVariant from './components/Attack-Variant.vue'
import DefendSocket from './components/Defend-Socket.vue'
import DefendVariant from './components/Defend-Variant.vue'
const currentAttackRef = ref('')
const defendedAttacks = ref(0)
const lastIncorrectDrop = ref(null)

//Successfully defended attacks counter
const incrementDefendedAttacks = (value) => {
  defendedAttacks.value += value
}

function handleIncorrectDrop(data) {
  lastIncorrectDrop.value = data
}
</script>

<template>
  <main>
    <section>
      <h1>🕷️ Attack Setup</h1>
      <AttackVariant @attackChanged="(currentAttack) => (currentAttackRef = currentAttack)" />
    </section>

    <section>
      <h1>🛡️ Defend Socket</h1>
      <DefendSocket
        :name="'Drop mechanism here'"
        :currentAttack="currentAttackRef"
        @increment="incrementDefendedAttacks"
        @incorrect="(data) => handleIncorrectDrop(data)"
      />
    </section>

    <section style="margin-top: 80px">
      <h1>🔒 Cyberattack Targets</h1>
      <div class="mechanism-pool">
        <DefendVariant
          v-for="name in [
            'User Accounts',
            'Licensing Systems',
            'Identities',
            'Data',
            'Web Session',
            'Network Integrity',
          ]"
          :key="name"
          :name="name"
          :targetHit="lastIncorrectDrop?.target === name"
        />
      </div>
    </section>

    <section>
      <h1>🧰 Mechanisms</h1>
      <div class="mechanism-pool">
        <DefendMechanism name="Encryption" />
        <DefendMechanism name="Authentication" />
        <DefendMechanism name="Authorization" />
        <DefendMechanism name="Web Application Firewall" />
        <DefendMechanism name="Network Segmentation" />
      </div>
    </section>

    <section>
      <h1>✅ Successfully Defended: {{ defendedAttacks }}</h1>
    </section>
  </main>
</template>

<style scoped>
main {
  padding: 2rem;
  font-family: sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.mechanism-pool {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}
section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}
</style>
