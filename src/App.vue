<template>
  <v-app :theme="theme">
    <v-app-bar>
      <v-btn to="/"> หน้าแรก </v-btn>
      <v-btn to="/form"> แบบฟอร์ม </v-btn>
      <v-btn to="/login"> เข้าสู่ระบบ </v-btn>
      <v-spacer></v-spacer>
      <v-btn
        :prepend-icon="
          theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'
        "
        @click="onClick"
        >Toggle Theme</v-btn
      >
    </v-app-bar>
    <v-main>
      <router-view> </router-view>
    </v-main>
  </v-app>
</template>
<script setup>
import { ref } from "vue";

const theme = ref("light");

function onClick() {
  theme.value = theme.value === "light" ? "dark" : "light";
}
</script>
<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
