<template>
  <div style="padding: 2px;">
    <v-btn>

      <v-icon class="icon">
        <slot name="icon"></slot>
      </v-icon>
      <slot name="label"></slot>

    </v-btn>
  </div>
</template>

<style>
.v-btn {
  min-height: 45px;
}

.icon {
  padding: 10px;
  padding-right: 30px
}
</style>