<template>
    <div id="user-profile">
    <!-- ich möchte auf daten aus meiner data() zugreifen -->
    <div class="user-profile__user-panel">
        <h1 class="user-profile__username">
            @{{ user.username }}
        </h1>
        <div class="user-profile__admin-batch" v-if="user.isAdmin">
            Admin
        </div>
        <div class="user-profile__follower-count">
            <strong>Followers: </strong> {{ followers }}
        </div>
    </div>
    <div class="user-profile__twoots_w" >
        <div class="user-profile__twoot" v-for="twoot in user.twoots" :key="twoot.id">
            {{twoot.content}}
        </div>
    </div>
  </div>
</template>

<script>
    export default {
      name: 'App',
      data() {
        return {
          followers: 0,
          user: {
            id: 1,
            username: 'SnowiSama',
            firstName: 'Snow',
            lastName: 'Sama',
            email: 'hcarsten1@googlemail.com',
            isAdmin: true,
            twoots: [
                {id: 1, content: "Twotter is Amazing"},
                {id: 2, content: "Don't forget to subscripe to my channel!"}
            ]
          }
        }
      },
      watch: {
        followers(newFollowerCount, oldFollowerCount) {
          if (oldFollowerCount < newFollowerCount) {
            console.log(`${this.user.username} has gained a follower!`);
          }
        }
      },
      computed: {
        fullName() {
          return `${this.user.firstName} ${this.user.lastName}`
        }
      },
      methods: {
        followUser() {
          this.followers++
        }
      },
      mounted() {
        this.followUser()
      }
    }
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 30%;
    padding: 50px 5%;   
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    width: 20%;
}

.user-profile__admin-batch {
    background: rebeccapurple;
    color: #fff;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

h1 {
    margin: 0;
}
</style>