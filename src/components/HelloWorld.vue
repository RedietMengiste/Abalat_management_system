<template>

<div class="spacing-playground pa-10">
  <v-data-table
    
    :headers="headers"
    :items="students"
    sort-by="calories"
    :search="search"
    class="elevation-1"
    
  >


    <template v-slot:top >
      <v-toolbar
      class="deep-purple lighten-1 rounded-t-xl"
        flat
      >
        <v-toolbar-title class="white--text text-h5 titleone">Abalat Registration Management System</v-toolbar-title>
        <v-divider
          class="mx-10"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        prepend-icon="mdi-magnify"
        label="Search"
        class="green lighten-5 pa-1 ma-6 rounded-xl elevation-1"
        single-line
        hide-details
      ></v-text-field>
        <v-dialog
         
          v-model="dialog"
          max-width="900px"
         
        >



          <template v-slot:activator="{ on, attrs } ">
            <v-btn
              
              color="white"
              class="mb-2 rounded-pill green lighten-5 green--text text--darken-2 pa-5 mr-10 mt-2"
              v-bind="attrs"
              v-on="on"
              
            ><v-icon
        Dense
        color="gren darken-1"
        class="mr-2 "
        @click="editItem(item)"
      >
        mdi-plus
      </v-icon>
              Register Student
            </v-btn>
          </template>




          <v-card class="rounded-xl" color="deep-purple lighten-5"> 
            <v-card-text>
              <v-container >
                <v-row>
                   <v-col
                   
                   cols="12"
                    sm="6"
                    md="4"
                    offset="5"
                    >
                    
                     <v-img
                  height="150px"
                  width="150px"
                  src="../assets/user.png"
                  
                ></v-img>
                  </v-col>
                </v-row>
                <v-row >
                 
                  <v-col
                  
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                    prepend-icon="mdi-account-circle"
                      v-model="editedItem.name"
                      label="Full Name"
                      color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      prepend-icon="mdi-gender-male-female"
                      v-model="editedItem.gender"
                      label="Gender"
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                    prepend-icon="mdi-phone"
                      v-model="editedItem.phone_number"
                      label="Phone No."
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                    prepend-icon="mdi-school"
                      v-model="editedItem.batch"
                      label="Batch/Year"
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                   <v-text-field
                    prepend-icon="mdi-card-account-details-outline"
                      v-model="editedItem.student_id"
                      label="ID"
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field></v-col>
                      <v-col
                  
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                    prepend-icon="mdi-google-classroom"
                      v-model="editedItem.dept"
                      label="Department"
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                  <v-col
                  
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                    prepend-icon="mdi-account-tie"
                      v-model="editedItem.ye_niseha_abat"
                      label="Ye Niseha Abat"
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                  <v-col
                  
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                    prepend-icon="mdi-account-network"
                      v-model="editedItem.muya_kifil"
                      label="Muya Kifil"
                       color="purple darken-5 purple--text text--darken-2"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                class="mb-2 rounded-pill red lighten-5 red--text text--darken-2 pa-5 mt-2"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
               
                class="mb-2 rounded-pill green lighten-5 green--text text--darken-2 pa-5 mr-10 mt-2"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>


        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5 purple lighten-5 purple--text text--darken-5">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn class="mb-2 rounded-pill green lighten-5 green--text text--darken-2 pa-5 mr-10 mt-2" text @click="closeDelete">Cancel</v-btn>
              <v-btn class="mb-2 rounded-pill red lighten-5 red--text text--darken-2 pa-5 mt-2" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>

    <template v-slot:item.actions="{ item }">
      <v-icon
        Dense
        color="deep-purple darken-1"
        class="mr-2 "
        @click="editItem(item)"
      >
        mdi-account-edit
      </v-icon>
      <v-icon
        color="deep-purple darken-1"
        Dense
        @click="deleteItem(item)"
      >
        mdi-delete-empty
      </v-icon>
    </template>


    <template v-slot:no-data>
      <v-btn
        color="deep-purple lighten-1"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>


  </v-data-table>
  </div>
</template>



// ''''''''''''''''''''''''''scripts'''''''''''''''''''''''''''''''''''''''''

<script>
  export default {
    data: () => ({
      search: '',
      dialog: false,
      dialogDelete: false,
      headers: [
        {
          text: 'Name',
          align: 'start',
          sortable: true,
          value: 'name',
        },
        { text: 'Gender', value: 'gender' },
        { text: 'Phone No.', value: 'phone_number' },
        { text: 'Batch', value: 'batch' },
        { text: 'Department', value: 'dept' },
        { text: 'ID', value: 'student_id' },
        { text: 'Ye Niseha Abat', value: 'ye_niseha_abat' },
        { text: 'Muya Kifil', value: 'muya_kifil' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      students: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        gender: '',
        phone_number: '',
        dept: '',
        student_id: '',
        ye_niseha_abat: '',
        muya_kifil:'',
      },
      defaultItem: {
        name: '',
        gender: '',
        phone_number: '',
        dept: '',
        student_id: '',
        ye_niseha_abat: '',
        muya_kifil:'',
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Add New Student' : 'Edit Profile'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.students = [
          {
            name: 'Rediet',
            gender: 'F',
            phone_number : '00',
            batch : '10',
            dept:'Software Engineering',
            student_id:'ATR/5890/10',
            ye_niseha_abat : 'Dn. Zerihun',
            muya_kifil :'Mezmur',
          },
          {
            name: 'Desta',
            gender: 'M',
            phone_number : '02323450',
            batch : '10',
            dept:'Chemical Engineering',
            student_id:'ATR/3456/10',
            ye_niseha_abat : 'Dn. Henok',
            muya_kifil :'It and Design',
          },
          {
            name: 'Lewi',
            gender: 'M',
            phone_number : '034560',
            batch : '10',
            dept:'Biomedical Engineering',
            student_id:'ATR/1234/10',
            ye_niseha_abat : 'Dn. Zelalem',
            muya_kifil :'Mezmur',
          },
          
        ]
      },

      editItem (item) {
        this.editedIndex = this.students.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.students.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
        this.students.splice(this.editedIndex, 1)
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.students[this.editedIndex], this.editedItem)
        } else {
          this.students.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>


