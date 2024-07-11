<template>
  <div id="app">
    <Conversion />
    <h1>Cuestionario</h1>
    <table class="questions-table">
      <thead>
        <tr>
          <th>Preguntas</th>
          <th>Respuestas</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <strong>Pregunta 1/5</strong><br>
            ¿Qué es Axios?
          </td>
          <td>
            a) Es una librería de Storage<br>
            <span :class="checkAnswer('b', '1')">b) Es una biblioteca de cliente http</span><br>
            c) Maneja la comunicación entre los componentes<br>
            d) Configura el routing de mi aplicación Vue.js
          </td>

          </tr>
        <tr>
          <td>
            <strong>Pregunta 2/5</strong><br>
            ¿Cuál es la forma correcta para registrar un evento de click en Vue.js?
          </td>
          <td>
            a) :click<br>
            <span :class="checkAnswer('b', '2')">b) @click</span><br>
            c) v-on@click<br>
            d) v-on:click<br>
            e) v-bind:click
          </td>
        </tr>
        <tr>
          <td>
            <strong>Pregunta 3/5</strong><br>
            Con Axios se pueden implementar los verbos:
          </td>
          <td>
            a) Solo Post<br>
            b) Solo Post y Get<br>
            <span :class="checkAnswer('c', '3')">c) Get, Post, Put y Delete</span><br>
            d) Solo Put
          </td>
        </tr>
        <tr>
          <td>
            <strong>Pregunta 4/5</strong><br>
            ¿Cuál de estas directivas se utiliza para modificar estilos a través de Vue.js?
          </td>
          <td>
            a) v-bind:src<br>
            <span :class="checkAnswer('e', '4')">b) v-bind:style</span><br>
            c) v-class<br>
            d) v-style<br>
            e) :style
          </td>
        </tr>
        <tr>
          <td>
            <strong>Pregunta 5/5</strong><br>
            ¿Qué función cumple el modificador number aplicado a v-model?
          </td>
          <td>
            <span :class="checkAnswer('a', '5')">a) Permite transformar la entrada de un elemento en un número</span><br>
            b) Es un validador HTML5<br>
            c) Modifica el dato de entrada para guardarlo como número en la propiedad vinculada<br>
            d) Convierte al número ingresado en una cadena de texto
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Conversion from './components/ConverterUsd.vue';

export default {
  name: 'App',
  components: {
    Conversion
  },
  methods: {
    checkAnswer(correctAnswer) {
      return {
        'correct-answer': this.selectedAnswer === correctAnswer,
        'incorrect-answer': this.selectedAnswer !== correctAnswer && this.selectedAnswer !== null
      };
    }
  }
};
</script>


<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.questions-table {
  width: 80%;
  margin: 20px auto;
  border-collapse: collapse;
}

.questions-table th, .questions-table td {
  border: 1px solid #ccc;
  padding: 10px;
}

.questions-table th {
  background-color: #f2f2f2;
}

.questions-table strong {
  font-weight: bold;
}

.correct-answer {
  color: green;
  font-weight: bold;
}

.incorrect-answer {
  color: red;
  font-weight: bold;
}
</style> npm