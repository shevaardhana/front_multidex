<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-alert
          dense
          text
          type="success"
          class="mb-5"
          dismissible
          :value="alert"
        >
          Thank you for your rate
        </v-alert>

        <v-card
          class="elevation-16 mx-auto"
          max-width="500"
          shaped
        >
          <v-card-title class="text-h5 px-5">
            <v-progress-linear :value="rating * 20" color="purple" rounded height="5" class="my-5" ></v-progress-linear>
            <h4>How would you rate your <br>
            satisfaction with our product ?</h4>
          </v-card-title>
          <v-card-text>
            <div class="text-center mt-3">
              <v-rating
                v-model="rating"
                color="grey"
                size="50"
                background-color="grey lighten-3"
                empty-icon="$ratingFull"
                half-increments
                hover
              ></v-rating>
              <span v-for="index in 5" :key="index" class="mx-6 text-h6">
                {{ index }}
              </span>
            </div>



            <v-row class="mt-2 mb-5">
              <v-col cols="6" class="text-center">
                <h4>Very dissatisfied</h4>
              </v-col>

              <v-col cols="6" class="text-center">
                <h4>Very satisfied</h4>
              </v-col>
            </v-row>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions class="justify-end">
            <v-btn
              color="purple"
              text
              @click="submit"
            >
              Submit
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>

      <v-col cols="8" class="text-right ml-12">
        <v-btn 
          text color="purple"
          @click="dashboard"
        >
          <u>Go to dashboard</u>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'RatingForm',

    data: () => ({
      rating: 4.0,
      alert: false,
    }),

    methods: {
      submit() {
        axios.post('http://127.0.0.1:8000/ratings/', {
          star: this.rating
        }).then(() => {
          this.alert = true;
        }).catch(() => {
          console.log(this.rating);
        });
      },

      dashboard() {
        this.$router.push('/dashboard'); 
      }
    }
  }
</script>