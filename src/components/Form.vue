<template>
  <form class="form">
    <input class="form__elem" type="text" v-model="title" placeholder="Заголовок">
    <input class="form__elem" type="text" v-model="description" placeholder="Описание">
    <select class="form__elem dark" v-model="status">
      <option value="Выполнено">Выполнено</option>
      <option value="В работе">В работе</option>
      <option value="Старт">Старт</option>
    </select>
    <input class="form__elem form__submit" type="submit" value="Создать" v-on:click="onSubmit">
  </form>
</template>

<script>
  export default {
    name: 'Form',
    data() {
      return {
        title: '',
        description: '',
        status: '',
        id: 0,
      }
    },
    methods: {
      onSubmit(e) {
        e.preventDefault();
        this.id++;
        this.$emit('add', {
          title: this.title,
          description: this.description,
          status: this.status,
          id: this.id,
        })
      }
    }
  }
</script>

<style>
  .form {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 400px;
    padding: 20px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.4);
    background-color: rgba(0, 0, 0, 0.2);
    box-sizing: border-box;
  }

  .form__elem {
    width: 100%;
    height: 30px;
    margin-bottom: 20px;
    padding-left: 20px;
    background-color: transparent;
    color: #ffffff;
    border: none;
    box-shadow: 0 0 5px rgba(255, 255, 255, 0.9);
    box-sizing: border-box;
    outline: none;
  }

  .dark {
    color: #42b983;
  }

  .form__elem::placeholder {
    color: #ffffff;
  }

  .form__submit {
    padding-left: 0;
    color: #ffffff;
  }

  @media (max-width: 700px) {
    .form {
      width: 100%;
      padding: 10px;
    }
  }
</style>
