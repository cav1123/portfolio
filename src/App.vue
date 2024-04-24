<template>
  <v-app>
    <v-container>
      <v-app-bar>
        <v-toolbar-title>
          <h1><router-link to="/">Home</router-link></h1>
        </v-toolbar-title>
        <v-spacer></v-spacer>
        <nav>
          <router-link to="/">Home</router-link>
          <router-link to="/about">About</router-link>
        </nav>
      </v-app-bar>
      <router-view />
    </v-container>
  </v-app>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
