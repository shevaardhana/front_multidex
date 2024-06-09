<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-card
          class="elevation-16 mx-auto"
          max-width="700"
        >
        
          <v-data-table
            :headers="headers"
            :items="ratings"
            :items-per-page="5"
            class="elevation-1"
          >
            <template v-slot:item="{ item }">
              <tr>
                <td>{{item.id}}</td>
                <td>{{ 'user ' + item.id }}</td>
                <td>
                  <v-rating
                    hover
                    length="5"
                    readonly
                    size="24"
                    :value=item.star
                    half-increments
                    color="purple"
                    background-color="purple accent-1"
                  ></v-rating>
                </td>
              </tr>
            </template>
          </v-data-table>
        </v-card>
      </v-col>

      <v-col cols="8" class="text-right">
        <v-btn 
          text color="purple"
          @click="form_rate"
        >
          <u>Go to form rate</u>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from 'axios';
  export default {
    name: 'DashboardTable',

    data () {
      return {
        headers: [
          {
            text: 'No',
            align: 'start',
            value: 'name',
          },
          { text: 'User', value: 'user' },
          { text: 'Rate / star', value: 'star' },
        ],

        ratings: []
      }
    },

    mounted() {
      axios.get('http://127.0.0.1:8000/ratings/').then((response) => {
        this.ratings = response.data;
      });
    },

    methods: {
      form_rate() {
        this.$router.push('/');
      }
    }
  }
</script>