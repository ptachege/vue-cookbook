<template>
   <div class="card my-3" v-for="note in all_notes" :key="note.id">
        <div class="card-body">
            <div class="d-flex justify-content-between align-items-center">
                <span>{{ note.note }}</span>
                <div>
                    <i class="fa-solid fa-edit me-4" @click="editNote(note.id)"></i>
                    <i class="fa-solid fa-trash " @click="deleteNote(note.id)"></i>
                </div>

            </div>
        </div>
    </div>
</template>
<script setup>

const props = defineProps({
  all_notes: Array
});

const emit = defineEmits(['deleteNote', 'editNote'])

function deleteNote(id){
    // emit delete to parent
    emit('deleteNote', id)
}

function editNote(id){
    console.log('edit note', id)

    emit('editNote', id)
}


</script>
<style lang="">
    
</style>