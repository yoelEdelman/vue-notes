<template>
    <section style="width: 90vw; margin: auto">
        <div v-if="!note.isEditing" style="margin: 10px auto; display: flex; justify-content: space-between">
            <div @dbclick="$emit('toEdit')"
                 v-if="!note.isEditing" style="padding-top: 5px; padding-left: 15px">
                {{ note.text }}
            </div>
            <div>
                <span style="color: #c3c3c3; font-size: 80%">{{ counterWord }}</span>

                <button style="justify-self: flex-end; align-self: flex-end; margin-right: 5px; color: dodgerblue; background: transparent" @click="$emit('toEdit')"><i class="fas fa-edit"></i></button>
                <button style="cursor:pointer;" @click="$emit('trash')" class="btn btn-danger">X</button>
            </div>
        </div>
        <div v-if="note.isEditing">
            <div>
                <textarea  v-model="note.text" class="forEdit" style="width: 100%;" v-focus ></textarea>

            </div>
            <article style="display: flex">
                <article style="width: 50%; text-align: center ">
                    <button @click="$emit('update')"
                            style=" font-size: 25px; color: #42b983; background: transparent">
                        <i class="fas fa-check-square"></i>
                    </button>
                </article>
                <article style="width: 50%; text-align: center"><button style=" font-size: 25px; color: #ff523c ; background: transparent" @click="$emit('notEdit')"><i class="fas fa-times-circle"></i></button></article>
            </article>

        </div>

    </section>
</template>


<style scoped>

    button{
        border: none;
    }

    div{
        background: #f6f6f6;
        border-radius: 10px;
    }


    .forEdit{
        border-top-right-radius: 10px;
        border-top-left-radius: 10px;

        border-top: 1px solid lightgray ;
        border-left: 1px solid lightgray;
        border-right: 1px solid lightgray;
        border-bottom: none;

        outline: none;
    }
</style>
<script>
    export default {
        name: "Todo",

        props:
            ['note']
        ,

        data(){
            return{
                note: this.note
            }
        },
        mounted(){

            console.log(this.note)
        },



        computed:{
            counterWord(){
                return this.note.text.trim().split(' ').length > 1 ? this.note.text.trim().split(' ').length + " words" : this.note.text.trim().split(' ').length + " word"
            }
        },

        directives: {
            focus: {
                inserted: function (el) {
                    el.focus()
                }
            }
        },
    }


</script>

