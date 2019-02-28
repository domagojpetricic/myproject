<template>
  <v-layout row>
    <v-flex sm4 pa-4>
      <v-toolbar color="yellow" dark>
        <v-toolbar-title>My Contacts</v-toolbar-title>
        <v-toolbar-title slot="extension" class="white--text">
          <v-icon dark>
            search
          </v-icon>
          <input 
            v-model="search" 
            type="text" 
            placeholder="Nađi kontakt"
          >
          </input>
        </v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-list two-line>
        <v-list-tile 
          v-for="user in filteredList" 
          :key="user.id" 
          active-class="highlighted"
        >
          <v-list-tile-content>
            <v-list-tile-title>
              <NuxtLink class="users-links" :to="'/users/'+user.id">
                {{ user.name }}
              </NuxtLink>
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-flex>
    <v-layout v-if="!isMobile()">      
      <v-flex pa-4>
        <NuxtChild :key="$route.params.id" />
      </v-flex>
    </v-layout>
  </v-layout>   
</template>

<script>
import axios from 'axios'
export default {
  computed: {
    filteredList() {
      return this.users.filter(user => {
        return user.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  },
  async asyncData() {
    const { data } = await axios.get(
      'https://jsonplaceholder.typicode.com/users'
    )
    return { users: data, search: '' }
  },
  methods: {
    isMobile() {
      if (
        /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
          navigator.userAgent
        )
      ) {
        return true
      } else {
        return false
      }
    }
  }
}
</script>

<style scoped>
.v-link-active {
  background-color: red;
}
.users-links {
  font-weight: bold;
  text-transform: uppercase;
  text-decoration: none;
  color: white;
}
.users-links:hover {
  color: yellow;
}
.v-list {
  height: 60vh;
  overflow-y: scroll;
}
::-webkit-scrollbar {
  width: 15px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #888;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
