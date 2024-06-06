
<template>
  <main>
    <div class="container mt-4">
      <h1>Home</h1>
      
      <p> Home / My Notes </p>


      <div class="row">
        <div class="col-6 offset-md-3">
          <div class="card">
            <div class="card-body">
              
              <div class="alert alert-warning text-center" v-if="all_notes.length == 0">
                 No notes found. 
              </div>

              <div v-else>

                <NoteList :all_notes="all_notes"  @deleteNote="deleteNote" @editNote="editNote"/>
                

              </div>

              <AddNote ref="addnoteref" @addNote="addNote" @updateNote="updateNote"/>

            </div>
          </div>
        </div>
      </div>
    </div>

  </main>
</template>


<script setup>
import { ref } from 'vue';
import AddNote from '@/components/AddNote.vue';
import NoteList from '@/components/NoteList.vue';

let all_notes = ref([])
const addnoteref = ref(null)

function addNote (note) {
  // create a new note object
  note = {
    id: all_notes.value.length + 1,
    note: note
  }
  all_notes.value.push(note)
}

function updateNote(note_obj, note){
  let note_ = all_notes.value.find(note => note.id === note_obj.id)
  note_.note = note
}

function deleteNote(id){
  all_notes.value = all_notes.value.filter(note => note.id !== id)
}

function editNote(id){
  let note = all_notes.value.find(note => note.id === id)
  addnoteref.value.setEditNote(note)
}

</script>
