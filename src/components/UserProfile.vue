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
            <strong>Followers: </strong> 
            {{ followers }}
        </div>
        <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot" >
            <label for="newTwoot">
                <strong>New Twoot:</strong> {{newTwootCharacterCount}} / 180
            </label>
            <textarea name="" id="newTwoot" cols="30" rows='4' maxlength="181" v-model="newTwootContent" :class="{'zuViel': newTwootCharacterCount > 180}"></textarea>
            <div class="user-profile__create-twoot-type">
                <label for="newTwootType">
                    <strong>Type: </strong>
                </label>
                <select name="" id="newTwootType" v-model="selectedTwootType">
                    <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
                        {{option.name}}
                    </option>
                </select>
            </div>
            <button :class="{'button__zuViel': newTwootCharacterCount > 180}" :disabled="newTwootCharacterCount > 180">
                Twoot!
            </button>
        </form>
    </div>
    <div class="user-profile__twoots-wrapper">
        <TwootItem 
        v-for="twoot in user.twoots" 
        :key="twoot.id" 
        :username="user.username" 
        :twoot="twoot" 
        @favourite="toggleFavourite"/>
    </div>
  </div>
</template>

<script>

import TwootItem from './TwootItem'

    export default {
      name: 'UserProfile',
      components: {
          TwootItem
      },
      data() {
        return {
            newTwootContent: '',
            selectedTwootType: 'instant',
            twootTypes: [
                {value: 'draft', name: 'Draft'},
                {value: 'instant', name: 'Instant Twoot'},
            ],
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
        },
        newTwootCharacterCount () {
          return this.newTwootContent.length;
        }
      },
      methods: {
        followUser() {
          this.followers++
        },
        toggleFavourite(id) {
            console.log(`Favourite Tweet #${id}`);
        },
        createNewTwoot() {
            if (this.newTwootContent && this.selectedTwootType !== 'draft') {
                this.user.twoots.unshift({
                    id: this.user.twoots.length + 1,
                    content: this.newTwootContent 
                }),
                this.newTwootContent=""
            }
        }
      },
      mounted() {
        this.followUser()
      }
    }
</script>

<style scoped>
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
    margin-bottom: 20px;
}

.user-profile__create-twoot {
    display: flex;
    flex-direction: column;
    border-top: 1px solid #DFE3E8;
    padding-top: 20px;
    
}

.user-profile__create-twoot .zuViel {
  border: 1px solid red;
  color: red;
}

.button__zuViel { 
  cursor: not-allowed;
  outline: none !important;
}


h1 {
    margin: 0;
}
</style>