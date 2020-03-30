<template>
  <div id="app">
    <TodoWrite  :notes="notes" />
    <div style="padding-top:60px">
      <Todo
              v-for="(not, index) in notes"
              :note="not"
              @notEdit="noEdit(not)"
              @trash="deleteItem(index)"
              @toEdit="toEdit(not)"
              @update="update(not)"
      />
    </div>

  </div>
</template>

<script>

  import TodoWrite from './components/NotesForm'
  import Todo from './components/NotesList'
  export default {
    name: 'app',
    components: {
      TodoWrite,
      Todo,
      props:[""]
    },

    data(){
      return{
        notes: [],
      }
    },
    mounted(){
      let data = localStorage.getItem('toDoList')
      if (!data){
        return
      }
      this.notes = JSON.parse(localStorage.getItem('toDoList'))
      console.log(this.notes)
    },
    methods:{

      deleteItem(elem){
        this.notes.splice(elem, 1); // supprime 1 élément à la position pos
        localStorage.setItem('toDoList', JSON.stringify(this.notes))
      },

      toEdit(elem){
        console.log(elem)
        elem.isEditing = true
        //  elem.isEditing = true
      },
      noEdit(elem){
        elem.isEditing = false
        // console.log(elem)
      },

      update(elem){

        if (elem.text.trim().length == 0){
          return
        }
        elem.isEditing = false
        localStorage.setItem('toDoList', JSON.stringify(this.notes))
      }
    }
  }
</script>

<style lang="scss">

</style>
