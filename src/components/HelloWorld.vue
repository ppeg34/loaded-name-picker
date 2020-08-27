<template>
  <v-container>
      <v-card
        v-if="names.length > 0" 
        class="mt-10 mb-5"
        cols="12"
      >
        <v-row class="px-3">
          <v-col v-for="(name, i) in names" :key="i" cols="4" class="px-6">
          <v-card class="pa-6 text-center">
            <h2 class="headline font-weight-bold mb-3">
              {{name}}
            </h2>
          </v-card>
          </v-col>
        </v-row>
        <v-col cols="12">
        </v-col>
      </v-card>
      <v-card>
        <v-row align="center" justify="center">
          <v-col cols="6">
          <v-text-field
            v-model="nameInput"
            label="Your name goes here"
            class=" px-6"
            @keydown.enter="addName()"
          ></v-text-field>
          </v-col>
            <v-col cols="2">
              <v-btn @click="addName()">Add Name</v-btn>
          </v-col>
        </v-row>

        <v-row justify="center">
          <v-dialog v-model="winnerPickDialog">
            <template v-slot:activator="{ on, attrs }">
              <v-btn 
                class="mb-6"
                v-bind="attrs"
                v-on="on"
                @click="pickWinner()"
              >Select Winner</v-btn>
            </template>

            <v-card>
              <v-row justify="center">
                <h1 class="my-16">
                  {{pickWinnerDisplay}}
                </h1>
              </v-row>
            </v-card>

          </v-dialog>
        </v-row>
      </v-card>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      nameInput: "",
      winnerPickDialog: false,
      loadedWinner: "Mikey",
      names: [],
      pickWinnerMessages: ["Reaching into the hat...", "Hey, thats not a name!!!", "Reaching back into my hat...", "Oh right I put them in the fish bowl, not my hat...", "Reaching into my fish bowl...", "and the winner is..." ],
      pickWinnerDisplay: "",
    }),
    methods: {
      addName () {
        this.names.push(this.nameInput);
        this.nameInput = "";
      },
      pickWinner () {
        this.winnerPickDialog = true;
        const getNextMessage = () => {
          setTimeout(() => {
            if (this.pickWinnerMessages.length > 0) {
              this.pickWinnerDisplay = this.pickWinnerMessages.shift();
              getNextMessage();
            } else {
              this.pickWinnerDisplay = `${this.loadedWinner}!!!`;
            }
          }, 3000);
        };
        this.pickWinnerDisplay = this.pickWinnerMessages.shift();
        getNextMessage();
      }
    }
  }
</script>
