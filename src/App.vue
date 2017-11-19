<template>
  <v-app dark>
    <v-content>
      <v-container>
        <v-layout>
          <v-flex>
            <v-card>
              <v-card-title id="quiz"> {{ currentQuestion.title }}</v-card-title>
              <v-card-text>
                {{ userAnswer }}
                <v-list>
                  <v-list-tile v-for= "(answer, answerIndex) in currentQuestion.answers"
                               :key="answerIndex"
                               v-on:click="getAnswerStatus(answerIndex)"
                  >
                    {{ answer }}
                  </v-list-tile>
                </v-list>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  import { quiz } from './quiz'

  export default {
    data () { 
    return {
      quiz: quiz,
      currentQuestionIndex: 0,
      userAnswer: null,
      name: '',
      surname: ''
    }
  },
    computed: {
      fullName () {
        return this.name + ' ' + this.surname
      },
      currentQuestion () {
        return quiz[this.currentQuestionIndex]
      }
    },
    methods: {
      getAnswerStatus (answerIndex) {
        if (this.userAnswer === null) {
          this.userAnswer = answerIndex;
          console.log(this.userAnswer);
        }
      }
    }
}
</script>

<style>
#app {

}
</style>
