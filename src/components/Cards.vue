<template>
  <div class="cards">
    <div class="filters" v-if="done">
      <div class="filters__categories">
        <p class="filtesr__descr" v-on:click="changeFilterTitle">
          Фильтрация по заголовку
        </p>
        <p class="filters__descr" v-on:click="changeFilterStatus">
          Фильтрация по статусу
        </p>
      </div>
      <div class="filters__body">
        <div class="filters__by-title" v-if="showFilters">
          <input class="filters__elem" type="text" v-model="filterTitle" placeholder="Введите заголовок">
        </div>
        <div class="filters__by-status" v-if="!showFilters">
          <input class="filters__elem" type="text" v-model="filterStatus" placeholder="Введите статус">
        </div>
      </div>
    </div>
    <div class="cards__body" v-if="done" v-bind:class="{'overflow-y': done}">
      <div class="cards__elem">
        <Card v-for="item in filteringTitle"
              v-bind:title="item.title"
              v-bind:description="item.description"
              v-bind:status="item.status"
              v-bind:id="item.id"
              :key="item.title"
              v-if="showFilters"
              @delete="removeCard"
              @changeStatus="changeStatus"
        />
        <Card v-for="item in filteringStatus"
              v-bind:title="item.title"
              v-bind:description="item.description"
              v-bind:status="item.status"
              v-bind:id="item.id"
              :key="item.title"
              v-if="!showFilters"
              @delete="removeCard"
              @changeStatus="changeStatus"
        />
      </div>
    </div>
    <Form @add="onAdding"/>
  </div>

</template>

<script>
  import Card from '@/components/Card.vue';
  import Form from '@/components/Form.vue';

  export default {
    name: 'Cards',
    components: {
      Card,
      Form
    },
    data() {
      return {
        items: [],
        filterTitle: '',
        filterStatus: '',
        done: false,
        flag: true,
        showFilters: true,
      }
    },
    computed: {
      filteringTitle() {
        let title = this.filterTitle;

        return this.items.filter((item) => {
          if (title === '') return true;
          else {
            console.log(item.title.indexOf(title));
            return item.title.indexOf(title) > -1;
          }
        });
      },
      filteringStatus() {
        let status = this.filterStatus;

        return this.items.filter((item) => {
          if (status === '') return true;
          else {
            console.log(item.status);
            return item.status.toLowerCase().indexOf(status.toLowerCase()) > -1;}
        });
      }
    },
    methods: {
      onAdding: function (data) {
        this.done = true;
        console.log(this.done);

        this.items.push({
          title: data.title,
          description: data.description,
          status: data.status,
          id: data.id,
        });
        console.log(data.status);
      },

      removeCard(data) {
        console.log(this.items);
        if(this.items.length === 1) {
          this.done = false;
          console.log(this.done);
        }

        this.items = this.items.filter(item => item.id !== data.id);
      },

      changeStatus(data) {
        let changedItems = this.items.filter(item => item.id === data.id);
        changedItems[0].status = data.status;
      },

      changeFilterTitle() {
        this.showFilters = true;
      },

      changeFilterStatus() {
        this.showFilters = false;
      }
    }
  }
</script>

<style>
  .cards {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .cards__body {
    max-height: 250px;
    margin-bottom: 20px;
    padding: 5px;
  }

  .cards__body::-webkit-scrollbar {
    width: 2px;
  }

  .cards__body::-webkit-scrollbar-track {
    box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  }

  .cards__body::-webkit-scrollbar-thumb {
    background-color: #42b983;
    outline: 1px solid slategrey;
  }

  .cards__elem {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .filters {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
  }

  .filters__categories {
    display: flex;
    justify-content: space-between;
    width: 400px;
  }

  .filters__body {
    display: flex;
    justify-content: center;
    width: 400px;
  }

  .filters__elem {
    height: 30px;
    padding: 10px;
    border: none;
    box-sizing: border-box;
    box-shadow: 0 0 5px rgba(255, 255, 255, 0.9);
    background-color: transparent;
  }

  .filters__elem::placeholder {
    color: #ffffff;
  }

  @media (max-width: 700px) {
    .cards, .cards__body {
      width: 100%;
    }

    .filters__categories {
      flex-direction: column;
      width: 100%;
      padding: 10px;
    }

    .filters__body {
      width: 100%;
      padding: 10px;
    }
  }

  .overflow-y {
    overflow-y: scroll;
  }

</style>
