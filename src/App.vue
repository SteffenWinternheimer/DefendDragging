<script setup>
import { ref } from 'vue'
import DefendMechanism from './components/Defend-Mechanism.vue'
import AttackVariant from './components/Attack-Variant.vue'
import DefendSocket from './components/Defend-Socket.vue'
import DefendVariant from './components/Defend-Variant.vue'
const currentAttackRef = ref('')
const defendedAttacks = ref(0)
const incrementDefendedAttacks = (value) => {
  defendedAttacks.value += value
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
      />
    </section>

    <section style="margin-top: 150px">
      <h1>🔒 Cyberattack Targets</h1>
      <div class="mechanism-pool">
        <DefendVariant name="User Accounts" />
        <DefendVariant name="Licensing Systems" />
        <DefendVariant name="Identities" />
        <DefendVariant name="Data" />
        <DefendVariant name="Web Session" />
        <DefendVariant name="Network Integrity" />
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
