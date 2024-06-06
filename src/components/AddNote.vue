<template >
    <div class="row">
        <div class="col-12">
            <p v-if="editing_mode">Edit Clicked Note</p>
            <input type="text" v-model="note" class="form-control" placeholder="Add a note" />
        </div>
        
    </div>

    <div class="d-flex justify-content-end">
        <button class="btn mt-2 me-4 float-right" :class="editing_mode ? 'btn-warning' : 'btn-primary'"  @click="addNote" >
            {{ editing_mode ? 'Update Note' : 'Add Note'}}
        </button>
        <button v-if="editing_mode" class="btn btn-dark mt-2"  @click="discardEdit" >
            Cancel
        </button>
    </div>
</template>
<script setup>
import { ref } from 'vue';


const emit = defineEmits(['addNote', 'updateNote'])


let note = ref('')
let editing_mode = ref(false)


// this is emiting an event back to the parent. in the parent will listen to this using @addNote

function addNote(){

    if (!note.value) {
        return alert('Please add a note')
    }
    if (editing_mode.value) {
        emit('updateNote', selectedNote.value, note.value)
        editing_mode.value = false
        note.value = ''
        selectedNote.value = null
        return
    }


    emit('addNote', note.value)
    note.value = ''
}


let selectedNote = ref(null)

function setEditNote(note_){
    note.value = note_.note
    selectedNote.value = note_
    editing_mode.value = true
}


function discardEdit(){
    note.value = ''
    editing_mode.value = false
    selectedNote.value = null
}
defineExpose({
    setEditNote
})


</script>
<style lang="">
    
</style>