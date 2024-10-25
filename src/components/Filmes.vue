<template>
  <div class="container">
    <h1 class="title">FILMES</h1>

    <div class="form">
      <div>
        <label>Título</label>
        <input v-model="titulo" required />
      </div>
      <div>
        <label>Gênero</label>
        <input v-model="genero" />
      </div>
      <div>
        <label>Ano de lançamento</label>
        <input v-model="ano" />
      </div>
      <button @click="submit">Salvar</button>
    </div>

    <div class="filmes">
      <template v-if="filmes.length === 0">
        <h3>Lista vazia</h3>
      </template>
      <template v-else>
        <div>
          <template v-for="(filme, index) in filmes" :key="index">
            <p>
              Título: {{ filme.titulo }} || Gênero: {{ filme.genero }} || Ano: {{ filme.ano }}
              <button class="delete-button" @click="deleteFilme(index)">Deletar</button>
            </p>
          </template>
        </div>
      </template>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';

const titulo = ref('');
const genero = ref('');
const ano = ref('');
const filmes = reactive([]);

function submit() {
  if (titulo.value.length === 0) {
    alert('Preencha o título do filme');
    return;
  }
  if (genero.value.length === 0) {
    alert('Preencha o gênero do filme');
    return;
  }
  if (ano.value.length === 0) {
    alert('Preencha o ano do filme');
    return;
  }

  filmes.push({
    titulo: titulo.value,
    genero: genero.value,
    ano: ano.value,
  });

  titulo.value = '';
  genero.value = '';
  ano.value = '';
}

function deleteFilme(index) {
  filmes.splice(index, 1);
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  min-width: 100vh;
  background: linear-gradient(to bottom, #ffccff, #ff99cc);
  padding: 20px;
  box-sizing: border-box;
}
.title {
  font-size: 3em;
  margin-bottom: 30px;
  color: #333;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.form div {
  margin-bottom: 15px;
  width: 100%;
}

label {
  font-size: 1.2em;
  margin-bottom: 3px;
  display: block;
}

input {
  padding: 12px;
  border-radius: 10px;
  border: 1px solid #ccc;
  width: 250px;
  font-size: 1.1em;
}

button {
  padding: 12px 28px;
  border-radius: 10px;
  background-color: #d5006d;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 1.1em;
}

button:hover {
  background-color: #c4005c;
}

.filmes {
  text-align: center;
}

.filmes p {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1.1em;
}

.delete-button {
  background-color: red;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
  margin-right: 0;
}

.delete-button:hover {
  background-color: darkred;
}
</style>
