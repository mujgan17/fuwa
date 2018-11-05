<template>
 
    <v-content v-if = "isOpen == 'true'">
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="#004D40">
                <v-toolbar-title>Login</v-toolbar-title>
                </v-toolbar>
              <v-card-text>
                <v-form>
                   <v-text-field label="username" single-line solo></v-text-field>
                  <v-text-field label="password" single-line solo></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="#004D40" @click = "isOpen= !isOpen">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>

</template>
<script> export default{
  name: 'app',
  props: {
    isOpen: String,
  },
  data: () => ({

  }),
  methods: {

  },

}
</script>
<style>
#app {
  height: 100%;
  background-color:#80CBC4;
  
}
</style>