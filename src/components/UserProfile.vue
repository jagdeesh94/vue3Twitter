<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.userName }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
          Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <form class="user-profile_create-twoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea  id="newTwoot" rows="4" v-model="newTwootContent"></textarea>
        <div class="user-profile_create-twoot-type">
          <label for="newTwootType"><strong>Type: </strong></label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option v-bind:value="option.value" v-for="(option,index) in twootTypes" :key="index">
              {{option.name}}
            </option> 
          </select>
        </div>
        <button>
          Twoot!
        </button>
      </form>
    </div>
    <div class="user-profile__twoots-wrapper">
        <TwootItem v-for="twoot in user.twoots" v-bind:key="twoot.id" :username="user.userName" :twoot="twoot" @favourite="toggleFavourite"/>
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem"
export default {
  name: "UserProfile",
  components:{
    TwootItem
  },
  data() {
    return {
      newTwootContent:'',
      selectedTwootType:'instant',
      twootTypes:[
        {value:"draft",name:"Draft"},
        {value:"instant",name:"Instant Twoot"}
      ],
      followers: 0,
      user: {
        id: 1,
        userName: "_MitchelRooney",
        firstName: "Mitchel",
        lastName: "Rooney",
        email: "aditirajendran94@gmail.com",
        isAdmin: true,
        twoots:[
            {
                id:1,content:"Twooter is amazing!"
            },
            {
                id:2,content:"Don't forget to use Twooter !"
            }
        ]
      },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id){
      console.log(`Tweet Favourited ${id}`);
    },
    createNewTwoot(){
      if(this.newTwootContent && this.selectedTwootType !== "draft"){
        //add twoots to the top of the list.push will add to the end of the list.
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent
        });
        this.newTwootContent = '';
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      console.log(
        "newFollowerCount,oldFollowerCount: ",
        newFollowerCount,
        oldFollowerCount
      );
      if (newFollowerCount < oldFollowerCount) {
        console.log(`${this.fullName}'s follower count reduced`);
      } else if (newFollowerCount > oldFollowerCount) {
        console.log(`${this.fullName}'s gained followers`);
      }
    },
  },
  mounted() {
    //this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}
.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}
.user-profile__admin-badge{
    background: purple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}
h1{
    margin: 0;
}
.user-profile__twoots-wrapper{
    display: grid;
    grid-gap: 10px;
}
.user-profile_create-twoot{
  display: flex;
  flex-direction: column;
  padding-top: 20px;
}
</style>