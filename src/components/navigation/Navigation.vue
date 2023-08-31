<script setup lang="ts">
import NavButton from './NavButton.vue';
import BitcoinFarm from '../icons/BitcoinFarm.vue'
</script>

<template>
  <v-container style="display: flex">
    <v-row no-gutters align="center" justify="center">
      <NavButton>
        <template #icon>
          <BitcoinFarm />
        </template>
        <template #label>
          Bitcoin Farm
        </template>
      </NavButton>
      <NavButton>
        <template #icon>
          <BitcoinFarm />
        </template>
        <template #label>
          Bitcoin Farm
        </template>
      </NavButton>
      <NavButton>
        <template #icon>
          <BitcoinFarm />
        </template>
        <template #label>
          Bitcoin Farm
        </template>
      </NavButton>
      <NavButton>
        <template #icon>
          <BitcoinFarm />
        </template>
        <template #label>
          Bitcoin Farm

        </template>
      </NavButton>
    </v-row>
  </v-container>
</template>

