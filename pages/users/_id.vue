<template>
  <v-layout>
    <v-flex>
      <v-card>
        <v-img src="https://www.ibts.org/wp-content/uploads/2017/08/iStock-476085198.jpg" aspect-ratio="2.5" />
        <v-card-title primary-title>
          <h3 class="headline mb-0">
            {{ name }}
          </h3>
        </v-card-title>
        <v-card-text mx-2 text-center>
          @{{ username }}<br><br>
          Email: {{ email }}<br><br>
          Adresa: Neka adresa...<br><br>
          Telefon: {{ phone }}<br><br>
          www: {{ website }}
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'
export default {
  validate({ params }) {
    return !isNaN(+params.id)
  },
  async asyncData({ params, error }) {
    try {
      const { data } = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${+params.id}`
      )
      return data
    } catch (e) {
      error({ message: 'User not found', statusCode: 404 })
    }
  }
}
</script>
