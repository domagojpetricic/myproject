<template>
  <v-layout row>
    <v-flex sm4 pa-3>
      <v-toolbar color="yellow" dark extended>
        <v-toolbar-title>My Contacts</v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-list two-line>
        <v-list-tile v-for="user in users" :key="user.id">
          <v-list-title>
            <NuxtLink :to="'/users/'+user.id">
              {{ user.name }}
            </NuxtLink>
          </v-list-title>
        </v-list-tile>
      </v-list>
    </v-flex>
    <v-layout>      
      <v-flex pa-3>
        <NuxtChild :key="$route.params.id" />
      </v-flex>
    </v-layout>
  </v-layout>   
</template>

<script>
import axios from 'axios'
export default {
  async asyncData() {
    const { data } = await axios.get(
      'https://jsonplaceholder.typicode.com/users'
    )
    return { users: data }
  }
}
</script>

<style scoped>
.v-list {
  height: 436px;
  overflow-y: auto;
}
</style>
