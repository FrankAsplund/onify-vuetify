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
        <v-form @submit.prevent="createUser">
    <v-container fluid>
      <v-row variant="outlined">
        <v-col
          cols="6"
          md="4"
        >
          <v-text-field
            :rules="nameRules"
            label="Förnamn"
            required
            v-model="formData.firstname"
            density="compact"
          ></v-text-field>
        </v-col>

        <v-col
          cols="6"
          md="4"
        >
          <v-text-field
            v-model="formData.lastname"
            :rules="nameRules"
            label="Efternamn"
            required
            density="compact"
          ></v-text-field>
        </v-col>
      </v-row>

        <v-row>
        <v-col
          cols="6"
          md="4"
        >
        <v-text-field
            v-model="formData.title"
            :rules="nameRules"
            label="Titel"
            required
            density="compact"
          ></v-text-field>
          </v-col>

          <v-col
          cols="6"
          md="4"
        >
        <v-text-field
            v-model="formData.phonenr"
            label="Telefon"
            required
            density="compact"
          ></v-text-field>
          </v-col>
      </v-row>

    </v-container>

      <v-container fluid>
    <v-row>
      <v-col cols="6" md="4">
        <v-autocomplete
    label="Company"
    :items= "companies"
    v-model="company"
    item-title="name"
    density="compact"
    height="100px"
    return-object
  ></v-autocomplete>
      </v-col>

      <v-col cols="6">
        <v-autocomplete
    label="Department"
    :items="company.tag"
    v-model="tag"
    item-title="tag"
    density="compact"
    
    return-object
  ></v-autocomplete>
      </v-col>


  <v-col cols="6">
        <v-autocomplete
    label="Select a system you're authorized in"
    :items= "items"
    v-model="formData.system"
    item-title="name"
    density="compact"
    multiple
  ></v-autocomplete>

      </v-col>
      <v-col cols="6">
        <v-combobox
          v-model="formData.system"
          label="Authorized Systems"
          chips
          multiple
          readonly
        ></v-combobox>
      </v-col>
    </v-row>
  </v-container>

      <v-btn
        color="success"
        class="mr-4"
        type="submit"
      >
        Submit
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
      formData: {
        firstname: "",
        lastname: "",
        title: "",
        phonenr: "",
        company: "",
        department: "",
        system: null,
      },

        /* systems: [], */
        items: [],
        companies: [],
        tag: [],
        company: {
          name: "",
          tag: "",
        },

      valid: false,
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      checkbox: false,
    }),

    methods: {

      async createUser() {
      const formData = {
        ...this.formData,
        company: this.company.name,
        department: this.company.tag,
      };
      try {
        // send POST request to create object endpoint
        const response = await fetch("http://localhost:8000/posts", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(formData),
        });
        //check for the status of the response
        if (!response.ok) {
          throw new Error(`Error ${response.status}`);
        }
        // object was successfully created, do something with the response data
      } catch (error) {
        // there was an error creating the object
        console.log(error);
      }
      /* console.log(response); */
      document.forms[0].reset();
      window.scrollTo(0, 0);
    },

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
          console.log(data.records);
      },

async getAllCompanies() {
      const response = await fetch(
        "https://oni-demo1-app.onify.net/api/v2/my/options/tags/company?pagesize=50&sort=name&sortby=asc",
          {
            headers: {
              accept: "application/json",
              authorization:
                "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJsaWEiLCJleHBpcmVkYXRlIjoiMjAyMy0wNC0zMFQwODo0NToyMC4wMDBaIiwiY2xpZW50Q29kZSI6Im9uaSIsImlhdCI6MTY3MTQzODE5MH0.0v8gGzhn5XQRswdeKF2AfGuCRh6EGj_HFQz2bupN5ao",
            },
          }
        )
        const data = await response.json();
        this.companies = data.records;

        console.log(data.records.tag);
        console.log(data.records);

        /* for (let i = 0; i < data.records.length; i++) {
            this.tags[i] = data.records[i].tag;
            console.log(data.records[i].tag);
        } */
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
    this.getAllCompanies();
    this.getAllSystems();
  }
}
</script>