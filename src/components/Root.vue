<template>
  <v-container>
    <v-card class="px-4 py-4">
      <form @submit.prevent="onSubmit">
        <v-row>
          <v-col cols="12">
            <h3 class="pb-2">File a Complaint</h3>
            <v-text-field
                label="Mail"
                outlined
                type="email"
                v-model="userData.email"
            ></v-text-field>
            <v-text-field
                @click:append="isShownPassword = !isShownPassword"
                v-model.lazy="userData.password"
                :append-icon="isShownPassword ? 'mdi-eye' : 'mdi-eye-off'"
                :type="isShownPassword ? 'text' : 'password'"
                name="input-10-1"
                hint="At least 8 characters"
                counter
                outlined label="Password"></v-text-field>
            <v-text-field v-model="userData.age" outlined label="Age"></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <!-- Interpolation between <textarea>{{ message }}</textarea> doesn't work!-->
            <v-textarea v-model="message" outlined label="Message"></v-textarea>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="2">
            <v-checkbox
                label="send mail"
                value="SendMail"
                color="success"
                hide-details
                v-model="selectedCheckboxes"
            ></v-checkbox>
          </v-col>
          <v-col cols="2">
            <v-checkbox
                label="send infomail"
                value="SendInfoMail"
                color="info"
                hide-details
                v-model="selectedCheckboxes"
            ></v-checkbox>
          </v-col>
          <v-col cols="2">
            <v-checkbox
                label="send SMS"
                value="SendSMS"
                color="warning"
                hide-details
                v-model="selectedCheckboxes"
            ></v-checkbox>
          </v-col>
        </v-row>
        <v-radio-group v-model="gender" row>
              <v-radio
                  label="male"
                  color="primary"
                  value="Male"
              ></v-radio>
              <v-radio
                  label="female"
                  color="error"
                  value="Female"
              ></v-radio>
        </v-radio-group>
        <v-select
            :items="items"
            label="Technology"
            return-object
            item-text="tech"
            outlined
            v-model="selectedTech"
        ></v-select>
        <v-btn type="submit" color="primary" dark>Submit</v-btn>
      </form>
    </v-card>
    <hr>

    <v-card class="px-4 py-4" v-if="isSubmitted">
      <v-card-title style="background: cornflowerblue">Your Data</v-card-title>
      <v-card-text style="border: 1px solid dodgerblue">
        <v-row>
          <v-col cols="12">
            <v-subheader>Mail: {{ userData.email }}</v-subheader>
            <v-subheader>Password: {{ userData.password }}</v-subheader>
            <v-subheader>Age: {{ userData.age }}</v-subheader>
            <v-subheader style="white-space: pre ">Message: {{ message }}</v-subheader>
            <ul>
              selected text boxes
              <v-subheader v-for="(item,i) in selectedCheckboxes" :key="i">* {{ item }}</v-subheader>
            </ul>
            <v-subheader>Gender: {{ gender }}</v-subheader>
            <v-subheader>Technology: {{ selectedTech.tech }}</v-subheader>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "appRoot",
  data: () => {
    return {
      userData: {
        email: '',
        password: '',
        age: 31
      },
      message: "test ",
      selectedCheckboxes: [],
      gender: 'Male',
      items:[{tech:'java'}, {tech:'nuxt'}, {tech:'vuetify'}],
      selectedTech:'',
      isSubmitted:false,
      isShownPassword: false
    }
  },
  methods: {
    onSubmit(){
      console.log("submit the form!")
      /* check if our form data is valid*/
    }
  }

}

</script>

<style scoped>

</style>
