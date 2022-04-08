<template>
  <div class="pa-6 text-center">
    <h1 class="teal--text ">Organiziere deinen Tag</h1>
    <h3 class="text--secondary teal--text text--lighten-2">Einfach und Stressfrei</h3>
    <v-divider class="ma-2"></v-divider>
    <v-text-field 
          class="pa-3" 
          label="Add a task" 
          hide-details 
          clearable
          v-model="newTaskTitle">
      <v-icon
        @click.stop="addTask"
        @keyup.enter="addTask"
        slot="append"
        color="green"
        class="mr-3">
      mdi-plus-circle-outline
      </v-icon>
    </v-text-field>
      <div class="d-flex pa-4 justify-space-around flex-wrap">
       <v-card
           max-width="475"
           class="ma-4">
       <v-toolbar
           color="teal"
           dark>
         <v-toolbar-title>Alle Aufgaben</v-toolbar-title>
       </v-toolbar>

       <v-list
           flat
           class="pt-0">
          <div 
             v-for="task in tasks"
             :key="task.id">
          <v-list-item class="text-left"
                       @click="doneTask(task.id)"
          >
            <template v-slot:default>
              <v-list-item-action>
                <v-checkbox
                   :input-value="task.done"
                    color="primary">
                </v-checkbox>
              </v-list-item-action>

              <v-list-item-content :class="{'text-decoration-line-through' : task.done}">
               <v-list-item-title>{{ task.title }}</v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn
                    @click.stop="deleteTask(task.id)" 
                    icon>
                 <v-icon color="red lighten-1">mdi-delete-circle-outline</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>
          </v-list-item>
            <v-divider></v-divider>
          </div>    
       </v-list>
       </v-card>
  
       <v-card
           max-width="475"
           class="ma-4">
         <v-toolbar
           color="teal"
           dark>
         <v-toolbar-title>Noch zu tun</v-toolbar-title>
        </v-toolbar>
        <v-list
          flat
          class="pt-0">
          <div 
             v-for="task in notDone"
             :key="task.id">
          <v-list-item class="text-left"
                       @click="doneTask(task.id)">
            <template v-slot:default>
             <v-list-item-content>
              <v-list-item-title>{{ task.title }}</v-list-item-title>
             </v-list-item-content>            
            </template>
          </v-list-item>
            <v-divider></v-divider>
          </div>
        </v-list>
       </v-card>

       <v-card
         max-width="475"
         class="ma-4">
         <v-toolbar
           color="teal"
           dark>
          <v-toolbar-title>Abgeschlossen</v-toolbar-title>
         </v-toolbar>
         <v-list
           flat
           class="pt-0">
          <div 
           v-for="task in done"
           :key="task.done">    
          <v-list-item class="text-left">
           <template v-slot:default>
            <v-list-item-content>
             <v-list-item-title>{{ task.title }}</v-list-item-title>
            </v-list-item-content>
           </template>
          </v-list-item>
            <v-divider></v-divider>
          </div>    
         </v-list>
       </v-card>
      </div>

  </div>
  
</template>

<script>

  export default {
    name: 'Home',
    data() {
      return {
        newTaskTitle: '',
        tasks: []
      }
    },
    methods: {
      addTask(){
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
          }
          this.tasks.push(newTask)
          this.newTaskTitle = ''
      },
      doneTask(id) {
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id != id)
      }
    },
    computed: {
      done(){
        return this.tasks.filter(task => task.done)
      },
      notDone(){
        return this.tasks.filter(task => !task.done)
      }
    }
  }
</script>
