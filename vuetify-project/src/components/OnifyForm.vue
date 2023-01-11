<template>
    <div class="d-flex align-center flex-row mx-4 pa-2">
      <v-card variant="tonal" class="mt-5 mb-8 rounded-sm" width="400">
        <v-card-title>Skapa användare</v-card-title>
      <v-card-text>
        Här kan du skapa dina egna användare, 
        komplett med namn, titel, företag, 
        och allt annat du skulle tänka dig!
      </v-card-text> 
      </v-card>
    </div>

    <div variant="outlined">
        <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="firstname"
            :rules="nameRules"
            :counter="10"
            label="First name"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="lastname"
            :rules="nameRules"
            :counter="10"
            label="Last name"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
        </v-col>
      </v-row>
    </v-container>

      <v-container fluid>
    <v-row>
      <!-- <v-col cols="12">
        <v-autocomplete
    label="Select a company"
    v-model="select"
    :items= "items"
    item-title="name"
    density="compact"
    multiple
  ></v-autocomplete>
      </v-col> -->
  <v-col cols="12">
        <v-autocomplete
    label="Select a system you're authorized in"
    v-model="select"
    :items= "items"
    item-title="name"
    density="compact"
    multiple
  ></v-autocomplete>

      </v-col>
      <v-col cols="12">
        <v-combobox
          v-model="select"
          label="I'm readonly"
          chips
          multiple
          readonly
        ></v-combobox>
      </v-col>
    </v-row>
  </v-container>

      <v-checkbox
        v-model="checkbox"
        :rules="[v => !!v || 'You must agree to continue!']"
        label="Do you agree?"
        required
      ></v-checkbox>
  
      <v-btn
        color="success"
        class="mr-4"
        @click="validate"
      >
        Validate
      </v-btn>
  
      <v-btn
        color="error"
        class="mr-4"
        @click="reset"
      >
        Reset Form
      </v-btn>
  
      <v-btn
        color="warning"
        @click="resetValidation"
      >
        Reset Validation
      </v-btn>
    </v-form>
</div>
  </template>

<script>
  export default {
    data: () => ({
        select: [],
        items: [""],

      valid: false,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],

      checkbox: false,
      
    }),

    methods: {

      /*  async getPosts() {

      const response = await fetch("http://localhost:8000/posts");
      const data = await response.json();
      this.items = data;
      console.log(data);
    }, */

   async getAllSystems() {
      const response = await fetch(
        "https://oni-demo1-app.onify.net/api/v2/my/items/access-management?filter=tag:system",
          {
            headers: {
              accept: "application/json",
              authorization:
                "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJsaWEiLCJleHBpcmVkYXRlIjoiMjAyMy0wNC0zMFQwODo0NToyMC4wMDBaIiwiY2xpZW50Q29kZSI6Im9uaSIsImlhdCI6MTY3MTQzODE5MH0.0v8gGzhn5XQRswdeKF2AfGuCRh6EGj_HFQz2bupN5ao",
            },
          }
        )
        const data = await response.json();

        for (let i = 0; i < data.records.length; i++) {
            this.items[i] = data.records[i].name;
}

      for (let i = 0; i < data.records.length; i++) {
          console.log(data.records[i].name);
    }
},

      async validate () {
        const { valid } = await this.$refs.form.validate()
        if (valid) alert('Form is valid')
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },

    mounted() {
    console.log("Mounted");
    /* this.getPosts(); */
    this.getAllSystems();
  }
}
</script>