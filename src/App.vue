<template>
  <v-app>
    <v-main>
      <div class="header">
        <v-row align="center" justify="center">
          <TarkovLogo></TarkovLogo>
        </v-row>
      </div>
      <Navigation />
      <div class="itemList">
        <v-list>
          <v-list-item v-for="(item, index) in    items   " :key="index" class="list-group-item">
            <v-row align="center" justify="center">
              <v-col>
                <v-img class="itemIcon" :src="item.iconLink"></v-img>
              </v-col>
              <v-col>
                {{ item.name }}
              </v-col>
              <v-col>
                {{ item.avg24hPrice.toLocaleString() }}
              </v-col>
            </v-row>
          </v-list-item>
          <v-list-item>
            <v-row align="center" justify="center">
              <v-col>

              </v-col>
              <v-col>

              </v-col>
              <v-col>
                {{ totalPrice }}
              </v-col>
            </v-row>
          </v-list-item>
        </v-list>
      </div>
      <div>
        <div class="col-md-12 text-center">
          <button @click="fetchItems" class="btn btn-md btn-primary">Refresh</button>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
import Navigation from './components/navigation/Navigation.vue';
import TarkovLogo from './components/icons/TarkovLogo.vue';
</script>

<script lang="ts">
import { defineComponent } from 'vue';
import { gql, request } from 'graphql-request'

interface ItemList<T> {
  items: T[]
}

interface ItemData {
  id: string,
  name: string,
  shortName: string,
  iconLink: string,
  avg24hPrice: number
}

export default defineComponent({
  name: 'MarketItems',
  data() {
    return {
      items: [] as ItemData[],
      totalPrice: 0,
    }
  },
  methods: {
    async fetchItems() {
      const query = gql`
      {
          items(names: ["t-plug", "bolts", "bleach"]) {
              id
              name
              shortName
              iconLink
              avg24hPrice
          }
      }
      `
      const response = await request('https://api.tarkov.dev/graphql', query)
      this.items = (response as ItemList<ItemData>).items;
      this.totalPrice = this.items.reduce((acc, item) => acc += item.avg24hPrice, 0);
    },
  },
  async mounted() {
    await this.fetchItems()
  }
})
</script>

<style>
.header {
  width: 50%;
  margin: auto
}

.itemList {
  width: 70%;
  margin: auto
}

.itemIcon {
  width: 50px;
  height: 50px;
}
</style>