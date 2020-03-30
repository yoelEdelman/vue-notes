<template>
    <div  class="input-group mb-3 headTop" style="width: 90vw;">
        <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">@</span>
        </div>
        <textarea style="height: 38px;" v-model="note"
                  @keyup.enter="send"
                  type="text"
                  class="form-control"
                  placeholder="To do"
        ></textarea>
        <article>
            <span class="counterNote" v-if="note"> {{counterNote}}</span>
        </article>
        <div class="input-group-prepend">
            <button @click='send'
                    class="btn btn-primary" style="border-top-right-radius: 5px; border-bottom-right-radius:5px" >Send</button>
        </div>
    </div>
</template>


<style scoped>

    textarea:focus,
    textarea.form-control:focus,
    input.form-control:focus,
    input[type=text]:focus,
    input[type=password]:focus,
    input[type=email]:focus,
    input[type=number]:focus,
    [type=text].form-control:focus,
    [type=password].form-control:focus,
    [type=email].form-control:focus,
    [type=tel].form-control:focus,
    [contenteditable].form-control:focus {
        box-shadow: inset 0 -1px 0 #ddd;
    }
</style>
<script>
    export default {
        name: "todoWrite",
        props :["notes"],
        data(){
            return{
                note: '',
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

        computed:{

            counterNote(){
                console.log(this.note.trim().split(' ').length )
                return this.note.trim().split(' ').length > 1 ? this.note.trim().split(' ').length + " words" :  this.note.trim().split(' ').length + " word"
            }
        },

        methods:{
            send(){
                if (this.note.trim().length == 0){
                    return
                }
                else{
                    let todo = {
                        id: Date.now(),
                        text: this.note,
                        isEditing: false,
                        check: false
                    }

                    this.notes.push(todo)
                    localStorage.setItem('toDoList', JSON.stringify(this.notes))
                    this.note =''
                    console.log(this.notes)
                }

            },
        }



    }
</script>

<style scoped>

    .headTop{
        position: fixed;
        top: 10px;
        left: 5vw;
    }

    .counterNote{

        position: absolute;
        z-index: 999999;
        right: 70px;
        top: 50%;
        transform: translateY(-50%);
        color: lightgray;

    }
</style>

