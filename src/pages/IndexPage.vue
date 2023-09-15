<template>
  <div class="row justify-center q-ma-md">
    <input type="text" v-model="todo" placeholder="Nova tarefa" />
    <button @click="salvar()" class="q-ml-sm">Adicionar</button>
  </div>
  <div class="row justify-between">
    <ul class="q-pa-md">
      <h3>Nova lista</h3>
      <li v-for="(item, index) in list" :key="index">
        {{ item }}
        <button class="cursor-pointer" @click="completeItem(index, item)">
          X
        </button>
        <button @click="editItem(index)">Editar</button>
      </li>
    </ul>
    <ul>
      <h3 class="q-mr-xl">Completas</h3>
      <li v-for="(item, index) in todoCompleta" :key="index">
        {{ item }}
        <button class="cursor-pointer" @click="deleteItem(index, item)">
          X
        </button>
      </li>
    </ul>
    <q-dialog v-model="showDialog">
      <q-card>
        <q-card-section>
          <div>Edit</div>
        </q-card-section>
        <q-card-section
          ><input type="text" v-model="editInput.item"
        /></q-card-section>
        <q-card-section
          ><q-btn label="Ok" @click="salvaEdit(index)"></q-btn
        ></q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
export default {
  name: "ToDoList",

  data() {
    return {
      todo: "",
      list: [],
      todoCompleta: [],
      editInput: {},
      showDialog: false,
    };
  },

  methods: {
    salvar() {
      this.list.push(this.todo);
    },

    completeItem(index, item) {
      this.list.splice(index, 1);
      this.todoCompleta.push(item);
    },

    deleteItem(index) {
      this.todoCompleta.splice(index, 1);
    },

    editItem(index) {
      this.showDialog = true;
      this.editInput.item = this.list[index];
      this.editInput.index = index;
    },

    salvaEdit() {
      this.list = this.list.map((item, index) => {
        if (index === this.editInput.index) {
          item = this.editInput.item;
        }
        return item;
      });
      this.showDialog = false;
    },
  },
};
</script>
