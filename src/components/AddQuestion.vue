<template>
  <v-dialog v-model="modalVisible">
    <v-btn slot="activator">Dodaj pytanie</v-btn>
    <v-card>
      <v-card-text>
        <v-form>
          <v-text-field
            label="add your question"
            v-model="newQ"></v-text-field>
          <v-text-field
            label="answer1"
            v-model="answer1"></v-text-field>
          <v-text-field
            label="answer2"
            v-model="answer2"></v-text-field>
          <v-text-field
            label="index poprawnej odp"
            type="number"
            min="0"
            max="1"
            v-model="correctIndex"></v-text-field>
          <p>Your Q: {{newQ}} </p>
          <v-card-actions>
            <v-btn @click="addQ">
              dodaj</v-btn>
          </v-card-actions>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    name: 'add-question',
    data() {
      return {
        newQ: null,
        answer1: null,
        answer2: null,
        correctIndex: null,
        modalVisible: false
      }
    },
    props: {numQuestions: {type: Number}},
    computed: {
      normalizeQuestion () {
        return {
          title: this.newQ,
          answers: [this.answer1, this.answer2],
          correctAnswerIndex: +this.correctIndex
        }
      }
    },
    methods: {
      addQ() {
        this.$emit('new-question', this.normalizeQuestion)
        this.$refs.form.reset()
      }
    }
  }
</script>


