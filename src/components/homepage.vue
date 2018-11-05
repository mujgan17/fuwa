<template>
  <v-app id="app">
    <v-toolbar dense color="#218c74" class="elevation-13">
      <v-toolbar-title class="mr-5 align-center">
        <span class="title white--text">
          <v-icon>🎼</v-icon> cuzy
        </span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-text-field append-icon="search" label="search a music" solo class="mt-2"
        v-model="searchAllFieldModel" @keyup.enter.native="searchAllFields()"></v-text-field>
      <v-spacer></v-spacer>

      <v-tooltip bottom>
        <v-btn slot="activator" dark fab color="grey" small @click="isAdding = !isAdding">
          <v-icon>add</v-icon>
        </v-btn>
        <span>add a music</span>
      </v-tooltip>
      <v-tooltip bottom>
        <v-btn slot="activator" dark fab color="grey" small @click="logout()">
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
          <td class="text-xs-right">{{ props.item.calories }}</td>
          <td class="text-xs-right">{{ props.item.fat }}</td>
          <td class="text-xs-right">{{ props.item.carbs }}</td>
          <td class="text-xs-right">{{ props.item.protein }}</td>
          <td class="text-xs-right">{{ props.item.iron }}</td>
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
  } from 'vuex';
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
            text: 'Dessert (100g serving)',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Calories', value: 'calories' },
          { text: 'Fat (g)', value: 'fat' },
          { text: 'Carbs (g)', value: 'carbs' },
          { text: 'Protein (g)', value: 'protein' },
          { text: 'Iron (%)', value: 'iron' }
        ],
        desserts: [
          {
            value: false,
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0,
            iron: '1%'
          },
          {
            value: false,
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3,
            iron: '1%'
          },
          {
            value: false,
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0,
            iron: '7%'
          },
          {
            value: false,
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3,
            iron: '8%'
          },
          {
            value: false,
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9,
            iron: '16%'
          },
          {
            value: false,
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0,
            iron: '0%'
          },
          {
            value: false,
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0,
            iron: '2%'
          },
          {
            value: false,
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5,
            iron: '45%'
          },
          {
            value: false,
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9,
            iron: '22%'
          },
          {
            value: false,
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7,
            iron: '6%'
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