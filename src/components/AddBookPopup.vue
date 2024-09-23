<template>
  <q-dialog v-model="localDialog" persistent>
    <q-card>
      <q-card-section>
        <div class="text-h6">Add a Book</div>
      </q-card-section>

      <q-card-section>
        <q-input v-model="bookName" label="Book Name" required lazy-rules
          :rules="[val => !!val || 'Name is required']" />
        <q-input v-model="numberOfPages" label="Number of Pages" type="number" required lazy-rules
          :rules="[val => val > 0 || 'Number of pages must be greater than 0']" />
      </q-card-section>

      <q-card-actions>
        <q-btn label="Cancel" color="secondary" @click="close" />
        <q-btn label="Add" color="primary" @click="addBook" :disabled="!isValid" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  name: 'AddBookPopup',
  props: {
    dialog: {
      type: Boolean,
      required: true
    }
  },
  setup(props, { emit }) {
    const bookName = ref('');
    const numberOfPages = ref(null);
    const localDialog = ref(props.dialog);

    const isValid = computed(() => {
      return bookName.value && numberOfPages.value > 0;
    });

    const close = () => {
      localDialog.value = false;
      bookName.value = '';
      numberOfPages.value = null;
      emit('update:dialog', false);
    };

    const addBook = () => {
      emit('book-added', { name: bookName.value, pages: numberOfPages.value });
      close();
    };

    // Watch for changes in the dialog prop
    watch(() => props.dialog, (newVal) => {
      localDialog.value = newVal;
    });

    return {
      localDialog,
      bookName,
      numberOfPages,
      isValid,
      close,
      addBook
    };
  }
};
</script>

<style scoped>
/* Optional styling */
</style>
