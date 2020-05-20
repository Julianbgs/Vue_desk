<template>
  <div class="card" v-bind:class="{'done': status === 'Выполнено', 'work': status === 'В работе', 'start': status === 'Старт'}">
    <div class="card__status">
      {{status}}
    </div>
    <div class="card__title">
      {{title}}
    </div>
    <div class="card__description">
      {{description}}
    </div>
    <div class="card__actions">
      <a href="#" class="card__delete" v-on:click="deleteCard">
        <img src="../assets/delete-begin.png" alt="">
      </a>
      <div class="card__change" v-on:click="openPopup">
        <p class="card__change-status">Изменить статус</p>
      </div>
    </div>
    <div class="modal" v-if="flag">
      <div class="modal__body">
        <div class="modal__close" v-on:click="closePopup">x</div>
        <form class="modal__form">
          <select class="modal__elem" v-model="changeStatus">
            <option value="Выполнено">Выполнено</option>
            <option value="В работе">В работе</option>
            <option value="Старт">Старт</option>
          </select>
          <input type="submit" value="Изменить" class="modal__elem modal__submit" v-on:click="change">
        </form>
      </div>
    </div>
    <div class="modal__overlay" v-on:click="closePopup" v-if="flag"></div>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: ['title', 'description', 'status', 'id', 'item'],
    data() {
      return {
        changeStatus: '',
        flag: false,
      }
    },
    mounted() {
      console.log(this.status);
    },
    methods: {
      deleteCard() {
        this.$emit('delete', {
          id: this.id
        });
      },
      openPopup() {
        this.flag = !this.flag

      },

      closePopup() {
        this.flag = !this.flag
      },
      change() {
        this.$emit('changeStatus', {
           status: this.changeStatus,
           id: this.id
        });
        this.flag = !this.flag;
      }
    },
  }
</script>

<style>

  .card {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 360px;
    margin-bottom: 20px;
    padding: 20px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.4);
  }

  .card:last-child {
    margin-bottom: 0;
  }

  .done {
    background-color: rgba(0, 128, 0, 0.5);
  }

  .work {
    background-color: rgba(128, 128, 0, 0.5);
  }

  .start {
    background-color: rgba(0, 128, 128, 0.5);
  }

  .card__description {
    margin-bottom: 10px;
  }

  .card__status {
    position: absolute;
    right: 10px;
    top: 10px;
    font-size: 14px;
  }

  .card__actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .card__delete {
    width: 25px;
    height: 25px;
  }

  .card__delete img {
    width: 100%;
    height: 100%;
  }

  .modal {
    position: fixed;
    top: 50%;
    left: 50%;
    z-index: 10;
    transform: translate(-50%, -50%);
  }

  .modal__overlay {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
  }

  .modal__body {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 350px;
    height: 250px;
    padding: 30px;
    background-color: #ffffff;
    z-index: 10;
  }
  .modal__close {
    position: absolute;
    top: 10px;
    right: 10px;
  }

  .modal__form {
    width: 250px;
  }

  .modal__elem {
    width: 100%;
    height: 30px;
    margin-bottom: 20px;
    padding-left: 20px;
    background-color: transparent;
    color: #42b983;
    border: 1px solid #42b983;
    box-shadow: 0 0 5px rgba(255, 255, 255, 0.9);
    box-sizing: border-box;
    outline: none;
  }

  .modal__elem::placeholder {
    color: #ffffff;
  }

  .modal__submit {
    padding-left: 0;
    color: #42b983;
  }

  @media (max-width: 700px) {
   .card {
     width: 100%;
   }

   .modal , .modal__form {
     width: 100%;
   }
   .modal__body {
     width: 100%;
     box-sizing: border-box;
   }
  }

</style>
