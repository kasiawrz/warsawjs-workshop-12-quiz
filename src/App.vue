<template>
  <v-app dark>
    <v-content>
      <v-container>
        <v-layout>
          <v-flex>
            <div class="success" v-if="userWon">
              GRATULACJE! Wygrałeś $ 1 000 000
            </div>
            <v-card>
              <v-card-title id="quiz"> {{ currentQuestion.title }}</v-card-title>
              <v-card-text>
                <v-list>
                  <v-list-tile v-for="(answer, answerIndex) in currentQuestion.answers"
                               :key="answerIndex"
                               @click="getAnswer(answerIndex)"
                               :class="getAnswerStatus(answerIndex)"
                  >
                    {{ answer }}
                  </v-list-tile>
                </v-list>
              </v-card-text>
              <v-card-actions>
                <v-btn v-if="isUserCorrect"
                       @click="getNextQuestion()"
                >
                  dalej</v-btn>
                <v-btn v-else="isUserCorrect"
                       @click="startAgain()"
                >
                  początek</v-btn>
              </v-card-actions>
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
      userWon: false
    }
  },
    computed: {
      currentQuestion () {
        return quiz[this.currentQuestionIndex]
      },
      isUserCorrect () {
        return this.currentQuestion.correctAnswerIndex === this.userAnswer
      }
    },
    methods: {
      getAnswer(answerIndex) {
        if (this.userAnswer === null) {
          this.userAnswer = answerIndex
        }
      },
      getAnswerStatus(answerIndex) {
        let index = this.currentQuestion.correctAnswerIndex;
        if (index === answerIndex && answerIndex === this.userAnswer) {
          if (index === this.quiz.length-1) {
            this.userWon = true
          }
          return "success"
        }
        else if (index !== answerIndex && answerIndex === this.userAnswer) {
          return "error"
        }
        else {
          return "secondary"
        }
      },
      getNextQuestion() {
        if (this.currentQuestionIndex < quiz.length-1) {
          this.currentQuestionIndex++
          this.userAnswer= null
        }
      },
      startAgain() {
        this.currentQuestionIndex = 0
        this.userAnswer= null
      }
    }
}
</script>

<style>
#app {

}
</style>
