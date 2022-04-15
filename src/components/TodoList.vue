<script>

export default {
  name: 'TodoList',
  data() {
    return {
      todoList: [],
      titre: '',
      nbHeures: '',
      responsable: '',
      id: 1,
    };
  },
  methods: {
    addToList() {
      if (this.titre !== '' && this.nbHeures > 0 && this.responsable !== '') {
        const todo = {};
        todo.titre = this.titre;
        todo.nbHeures = this.nbHeures;
        todo.responsable = this.responsable;
        todo.id = this.id;
        if (this.todoList.find((i) => i.id === todo.id) !== undefined) {
          this.todoList.splice(todo.id - 1, 1, todo);
        } else {
          this.todoList.push(todo);
        }

        this.titre = '';
        this.nbHeures = '';
        this.responsable = '';
        this.id += 1;
      } else {
        alert('impossible mec');
      }
    },
    deleteAll() {
      this.todoList = [];
    },
    edit(id) {
      console.log(id);
      const todo = this.todoList.find((i) => i.id === id);
      this.titre = todo.titre;
      this.nbHeures = todo.nbHeures;
      this.responsable = todo.responsable;
      this.id = todo.id;
    },
    deleteOne(id) {
      const todo = this.todoList.find((i) => i.id === id);
      this.todoList.splice(todo.id - 1, 1);
    },
  },
};
</script>

<template>
    <div>
        <label for="titre">Titre<input id="titre" v-model="titre" name="titre" type="text"></label>
        <label for="nbHeures">Nombre d'heures<input v-model="nbHeures" id="nbHeures"
        name="nbHeures" type="number">
        </label>
        <label for="responsable">Responsable
        <select id="responsables" v-model="responsable" name="responsable">
            <option value="Hugo">Hugo</option>
            <option value="Paul">Paul</option>
        </select></label>
        <button v-on:click="addToList">+</button>
        <button v-on:click="deleteAll">Tout supprimer</button>
        <div v-for="todo in todoList" :key="todo.id">
          <p>
            {{todo.titre}} {{todo.nbHeures}} {{todo.responsable}}
          </p>
          <button v-on:click="edit(todo.id)">Editer</button>
          <button v-on:click="deleteOne(todo.id)">Supprimer</button>
        </div>
    </div>
</template>
