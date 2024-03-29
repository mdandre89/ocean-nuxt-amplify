<template>
  <div class="middlealign text-container">
    <ul>
      <li>
        <p>
          This report estimates the individual's level on each of the five broad
          personality domains of the Big Five Aspects Scale.
        </p>
      </li>
      <li>
        <p>
          The description of each one of the five broad domains is followed by a
          more detailed description of personality according to the two
          subdomains that comprise each domain.
        </p>
      </li>
      <li>
        <p>
          These broad domains cover normal differences in personality that
          should be obvious to people who know you well.
        </p>
      </li>
      <li>
        <p>
          The inventory does not reveal hidden, secret information about you nor
          does it assess serious psychological disorders.
        </p>
      </li>
      <li>
        <p>
          The report is designed to be objective, not pleasing or flattering.
        </p>
      </li>
      <li>
        <p>
          Measurement error, misunderstandings, carelessness, and mischievous
          responding can invalidate the report.
        </p>
      </li>
      <li>
        <p>
          If knowledgeable acquaintances disagree with the test results, then
          the results are wrong.
        </p>
      </li>
      <li>
        <p>
          Your numerical scores are reported and graphed as percentile
          estimates. For example, a score of '60' means that your level on that
          trait is estimated to be higher than 60% of persons of your sex and
          age. Please keep in mind that 'low,' 'average,' and 'high' scores on a
          personality test are neither absolutely good nor bad.
        </p>
      </li>
    </ul>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="name"
        :rules="nameRules"
        :counter="10"
        label="Nickname"
        required
        outlined
      ></v-text-field>
      <v-select
        v-model="sex"
        :items="items"
        :rules="sexRules"
        label="Sex"
        outlined
        required
      ></v-select>
      <v-text-field
        v-model="age"
        :rules="ageRules"
        label="age"
        required
        outlined
        type="number"
      ></v-text-field>

      <v-btn class="mr-4" @click="submit"> submit </v-btn>
      <v-btn @click="clear"> clear </v-btn>
    </v-form>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'
export default {
  metaInfo: {
    title: 'Test - The Big Five Aspects Scale',
    titleTemplate: '%s | Free Personality Test',
  },
  data: () => ({
    valid: true,
    age: '',
    sex: null,
    name: '',
    items: ['male', 'female'],
    checkbox: false,
    nameRules: [
      (v) => !!v || 'Name is required',
      (v) =>
        (v && v.length <= 10) || 'Nickname must be less than 10 characters',
      (v) => (v && v.length >= 2) || 'Name must be at least 2 characters',
    ],
    sexRules: [(v) => !!v || 'Sex is required'],
    ageRules: [
      (v) => !!v || 'Age is required',
      (v) => (v && v < 95) || 'Age must be less than 95',
      (v) => (v && v > 10) || 'Age must be more than 10',
    ],
  }),

  methods: {
    ...mapMutations(['setSex', 'setAge']),
    submit() {
      if (this.$refs.form.validate()) {
        if (this.$route.path != '/test') {
          this.setSex(this.sex)
          this.setAge(this.age)
          this.$router.push({ path: `/test` })
        }
      }
    },
    clear() {
      this.$refs.form.reset()
    },
  },
}
</script>