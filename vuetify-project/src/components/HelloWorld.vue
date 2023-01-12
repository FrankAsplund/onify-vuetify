<template>
  <v-container class="fill-height">
    <v-responsive class="d-flex align-center text-center fill-height">
      <v-img
        contain
        height="300"
        src="@/assets/logo.svg"
      />

      <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>

      <h1 class="text-h2 font-weight-bold">Vuetify</h1>

      <div class="py-14" />

      <v-row class="d-flex align-center justify-center">
        <v-col cols="auto">
          <v-btn
            href="https://next.vuetifyjs.com/components/all/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text"
          >
            <v-icon
              icon="mdi-view-dashboard"
              size="large"
              start
            />

            Components
          </v-btn>
        </v-col>

        <v-col cols="auto">
          <v-btn
            color="primary"
            href="https://next.vuetifyjs.com/introduction/why-vuetify/#feature-guides"
            min-width="228"
            rel="noopener noreferrer"
            size="x-large"
            target="_blank"
            variant="flat"
          >
            <v-icon
              icon="mdi-speedometer"
              size="large"
              start
            />

            Get Started
          </v-btn>
        </v-col>

        <v-col cols="auto">
          <v-btn
            href="https://community.vuetifyjs.com/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text"
          >
            <v-icon
              icon="mdi-account-group"
              size="large"
              start
            />

            Community
          </v-btn>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script setup>
  
  /* Backup
  {
  "posts": [
    {
      "id": 1,
      "firstname": "Förnamn 1",
      "lastname": "Efternamn 1",
      "title": "CEO",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "id": 3,
      "firstname": "Förnamn 1",
      "lastname": "Efternamn 1",
      "title": "Front end developer",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "firstname": "Frank",
      "lastname": "Asplund",
      "title": "Praktikant",
      "phonenr": "0729067387",
      "company": "Onify",
      "department": "Front end",
      "id": 4
    },
    {
      "firstname": "Robert",
      "lastname": "Lundsten",
      "title": "CTO",
      "phonenr": "00000000000000",
      "company": "Test",
      "department": "Test",
      "id": 5
    },
    {
      "id": 6,
      "firstname": "Förnamn 6",
      "lastname": "Efternamn 6",
      "title": "Founder",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "id": 8,
      "firstname": "Förnamn 8",
      "lastname": "Efternamn 8",
      "title": "CEO",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "id": 9,
      "firstname": "Förnamn 9",
      "lastname": "Efternamn 9",
      "title": "Founder",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "id": 10,
      "firstname": "Förnamn 10",
      "lastname": "Efternamn 10",
      "title": "Front end developer",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "firstname": "Robin",
      "lastname": "Asplund",
      "title": "Praktikant",
      "phonenr": "0729067387",
      "company": "Onify",
      "department": "Front end",
      "id": 11
    },
    {
      "firstname": "Maria",
      "lastname": "Bergström",
      "title": "CEO",
      "phonenr": "00000000000000",
      "company": "Test",
      "department": "Test",
      "id": 12
    },
    {
      "id": 13,
      "firstname": "Förnamn 13",
      "lastname": "Efternamn 13",
      "title": "Founder",
      "phonenr": "123 456 789",
      "company": "Onify",
      "department": "IT"
    },
    {
      "firstname": "Daniel",
      "lastname": "Bladh",
      "title": "Praktikant",
      "phonenr": "0000000000",
      "company": "Onify",
      "department": "Front end",
      "id": 15
    },
    {
      "firstname": "Frank",
      "lastname": "Asplund",
      "title": "Praktikant",
      "phonenr": "0729067387",
      "company": "Min kommun Energi AB",
      "department": "Front end",
      "id": 17
    },
    {
      "firstname": "Frank",
      "lastname": "Asplund",
      "title": "Praktikant",
      "phonenr": "0729067387",
      "company": [
        "",
        "Other"
      ],
      "department": "Test",
      "system": "",
      "id": 18
    },
    {
      "firstname": "test",
      "lastname": "test",
      "title": "ttest",
      "phonenr": "test",
      "company": "Min kommun Fastigheter AB",
      "department": "access-management",
      "system": [
        "",
        "Pippin"
      ],
      "id": 20
    }
  ]
}




  */
</script>
