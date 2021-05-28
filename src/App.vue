<template>
<!-- mein html teil -->
  <UserProfile/>
</template>

<script>
/* mein javascript teil */
import UserProfile from './components/UserProfile'
export default {
  name: '#app',
  components: {
    UserProfile,
  }
}
</script>

<style>
/* mein css teil */
#app {
  font-family: Avenir, Helvetica, sans-serif;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
  padding: 50px;
}
</style>
