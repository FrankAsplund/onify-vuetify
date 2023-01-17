<template>
  <v-app class="mx-12 my-2 pa-6 rounded-m bg-grey-darken-4 align-items">
      <div class="d-flex align-center flex-row mx-4 pa-2 justify-center">
      <v-card variant="tonal" class="rounded-sm" width="500">
        <v-card-title>Skapa användare</v-card-title>
      <v-card-text>
        Här kan du skapa dina egna användare, 
        komplett med namn, titel, företag, 
        och allt annat du skulle tänka dig! <br>
        OBS: Alla fält är obligatoriska att fylla i.
      </v-card-text> 
      </v-card>
      </div>

<div variant="outlined">
<v-form @submit.prevent="createUser" ref="form" >
    <v-container fluid>
      <v-container>
      <v-row variant="outlined"  class="justify-center">
        <v-col
          cols="6"
          md="6"
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
          md="6"
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

        <v-row class="justify-center">
        <v-col
          cols="6"
          md="6"
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
          md="6"
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
    <v-row class="justify-center">
      <v-col cols="6" md="6">
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

      <v-col cols="6" md="6">
        <v-autocomplete
    label="Department"
    :items="company.tag"
    v-model="formData.department"
    item-title="tag"
    density="compact"
    return-object
  ></v-autocomplete>
      </v-col>
    </v-row>

      <v-row class="justify-center">
  <v-col cols="6" md="6">
        <v-autocomplete
    label="Select a system you're authorized in"
    :items= "systems"
    v-model="formData.system"
    item-title="name"
    density="compact"
    multiple
  ></v-autocomplete>

      </v-col>
      <v-col cols="6" md="6">
        <v-combobox
          v-model="formData.system"
          label="Authorized Systems"
          chips
          multiple
          readonly
          density="compact"
        ></v-combobox>
      </v-col>
    </v-row>
  </v-container>

  <v-row class="justify-center">
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
  </v-row>
          </v-container>
        </v-form>
      </div>
  </v-app>
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
        date: "",
      },

        systems: [],
        companies: [],
        company: {
          name: "",
        },

      valid: false,
      nameRules: [
        v => !!v || 'This field is required',
        v => v.length <= 20 || 'Name must be less than 20 characters',
      ],
      checkbox: false,
    }),

    methods: {

      async createUser() {

        // The date the user was created
        let currentDate = new Date();
        let date = currentDate.getFullYear()+'-'+(currentDate.getMonth()+1)+'-'+currentDate.getDate();
        let time = currentDate.getHours() + ":" + currentDate.getMinutes() + ":" + currentDate.getSeconds();
        let dateTime = date+' '+time;

      console.log("Denna användare skapades: ", dateTime);

      const formData = {
        ...this.formData,
        company: this.company.name,
        date: dateTime,
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
        console.log(response);
        // object was successfully created, do something with the response data
      } catch (error) {
        // there was an error creating the object
        console.log(error);
      }

      /* document.forms[0].reset(); */
      this.$refs.form.reset();
      console.log(this.formData);
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
            this.systems[i] = data.records[i].name;
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

        console.log(data.records);
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