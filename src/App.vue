<template>
  <div id="app">
    <div id="nav" class="lead bg-dark text-center text-light">
      <router-link to="/" class="text-light ">Home</router-link>
    </div>
    <router-view />

    <div class="container fixed-bottom text-center">
      <span class="text-muted">Created by Garrett Hensley</span>
    </div>
  </div>
</template>

<style>
body {
  background-color: #374e5a;
}
</style>
