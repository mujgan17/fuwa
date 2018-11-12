<template>
  <v-app id="app">
    <v-toolbar dense color="#218c74" class="elevation-15">
      <v-toolbar-title class="mr-5 align-center">
        <span class="title white--text">
          <v-icon>🎼</v-icon> fuwa
        </span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-text-field append-icon="search" label="search a music" solo class="mt-2"
        v-model="searchAllFieldModel" @keyup.enter.native="searchAllFields()"></v-text-field>
      <v-spacer></v-spacer>

      <v-tooltip bottom>
        <v-btn slot="activator" dark fab color="#d1ccc0" small @click="isAdding = !isAdding">
          <v-icon>add</v-icon>
        </v-btn>
        <span>add a music</span>
      </v-tooltip>
      <v-tooltip bottom>
        <v-btn slot="activator" dark fab color="#d1ccc0" small @click="logout()">
          <v-icon>exit_to_app</v-icon>
        </v-btn>
        <span>logout</span>
      </v-tooltip>
    </v-toolbar>

    <v-content>
      
    <v-data-table
      v-model="selected"
      :headers="headers"
      :items="desserts"
      :pagination.sync="pagination"
      select-all
      item-key="name"
      class="elevation-1"
    >
      <template slot="headers" slot-scope="props">
        <tr>
          <th>
             
          </th>
          <th
            v-for="header in props.headers"
            :key="header.text"
            :class="['column sortable', pagination.descending ? 'desc' : 'asc', header.value === pagination.sortBy ? 'active' : '']"
            @click="changeSort(header.value)"
          >
            <v-icon small>arrow_upward</v-icon>
            {{ header.text }}
          </th>
        </tr>
      </template>
      <template slot="items" slot-scope="props">
        <tr :active="props.selected" @click="props.selected = !props.selected">
          <td>
            <v-icon style="border:1px solid #333;border-radius:50%;cursor:pointer;background:#222;color:#fff;">play_arrow</v-icon>
          </td>
          <td>{{ props.item.name }}</td>
          <td class="text-xs-right">{{ props.item.length }}</td>
          <td class="text-xs-right">{{ props.item.vote }}    <template>
  <div class="text-xs-center">
    <v-rating v-model="rating"
    
    background-color="green lighten-3"
    color="green"
    ></v-rating>
  </div>
</template></td>
        </tr>
      </template>
    </v-data-table>
 
  
      <v-bottom-nav :active.sync="bottomNav" :value="true" absolute color="transparent" style="z-index:4">
        <v-btn color="white" flat value="recent">
          <span>last song played</span>
          <v-icon>history</v-icon>
        </v-btn>
        <v-btn color="white" flat value="favorites">
          <span>favorite songs</span>
          <v-icon>fav</v-icon>
        </v-btn>
      </v-bottom-nav>
    </v-content>
  </v-app>
</template>



<script>
  import axios from 'axios';
  import {
    mapState,
    mapActions,
    mapMutaions
  } 
  from 'vuex';
  import firebase from 'firebase';

  export default {

    data: () => ({
      drawer: true,
      leftNavbar: [{
          icon: "trending_up",
          text: "favorites"
        },
        {
          icon: "featured_play_list",
          text: "songs"
        }

      ],
      bottomNav: "recent",
      searchAllFieldModel: '',
      isAdding: false,
      searchModel: '',
      searchItems: [],
      searchLoading: false,
      searchText: null,
       headers: [
          {
            text: 'title',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'length', value: 'length' },
          { text: 'vote', value: 'vote'},
       
        ],
        desserts: [
          {
            value: false,
            title: 'Frozen Yogurt',
           
           
           
          },
          {
            value: false,
            title: 'Ice cream sandwich',
            
            
          },
          {
            value: false,
            title: 'Eclair',
       
          },
          {
            value: false,
            title: 'Cupcake',
            
     
            
          },
          {
            value: false,
            title: '',
            
    
            
          },
          {
            value: false,
            title: 'Jelly bean',
           
        
         
          },
          {
            value: false,
            title: 'Lollipop',
            
     
           
          },
          {
            value: false,
            name: 'Honeycomb',
          
          },
          {
            value: false,
            title: 'Donut',
            
      
          },
          {
            value: false,
            title: 'KitKat',
            
         
           
          }
        ]
    }),
  }
</script>
<style>
  #app {
    height: 100%;
    background-color: #c7ecee;

  }

  .v-input__control {
    min-height: 35px !important
  }
</style>
