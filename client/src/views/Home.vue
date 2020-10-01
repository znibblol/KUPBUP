<template>
  <div class="home">
    <section id="boards">
      <div class="container">
        <div class="filter">
          <div class="department-filter btn" @click="resetFilter()">Reset filter</div>
          <div class="department-filter" v-for="department in departments" :key="department.id">
          <div @click="filterBoards(department.id)">{{ department.name }}</div>
          </div>
        </div>
        <div class="board-wrapper">
          <router-link :to="board.href" class="board" v-for="(board, index) in boards" :key="index" :style="{background: 'url(' + board.background + ')', backgroundRepeat: 'no-repeat', backgroundSize: 'cover', backgroundPosition: 'center'}">
            <div class="text">
              <h4>{{ board.topic }}</h4>
              <h6>{{ board.description }}</h6>
            </div>
          </router-link>
        </div>
      </div>
    </section>

    <div id="toggle_form" @click="toggleForm()">+</div>


    <form id="add_form" @submit.prevent="addBoard()" class="add-form">
      <h3>Add a new board</h3>
      <div class="form-group">
        <label for="topic">Topic</label>
        <input type="text" name="topic" id="topic" class="form-text" v-model="newTopic">
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <input type="text" name="description" id="description" class="form-text" v-model="newDescription">
      </div>
      <div class="form-group">
        <label for="image">ImageUrl</label>
        <input type="text" name="image" id="image" class="form-text" v-model="newImage">
      </div>
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      departments: [
        {
          id: 1,
          name: 'Development'
        },
        {
          id: 2,
          name: 'Design'
        },
        {
          id: 3,
          name: 'Supplier'
        },
        {
          id: 4,
          name: 'Sales'
        }
      ],
      boards: [
        /* 
          departments:
          1: dev,
          2: design,
          3: supplier,
          4: sales
        */
        {
          topic: 'Lorem 1',
          description: 'lorem ipsum dolar',
          department: 1,
          background: 'https://source.unsplash.com/random/450x175/?winter',
          href: "board/lorem-1",
        },
        {
          topic: 'Lorem 2',
          description: 'lorem ipsum dolar',
          department: 2,
          background: 'https://source.unsplash.com/random/450x176?winter',
          href: "board/lorem-2",
        },
        {
          topic: 'Lorem 3',
          description: 'lorem ipsum dolar',
          department: 3,
          background: 'https://source.unsplash.com/random/451x175?winter',
          href: "board/lorem-3",
        },
        {
          topic: 'Lorem 4',
          description: 'lorem ipsum dolar',
          department: 4,
          background: 'https://source.unsplash.com/random/451x176?winter',
          href: "board/lorem-4",
        },
        {
          topic: 'Lorem 5',
          description: 'lorem ipsum dolar',
          department: 2,
          background: 'https://source.unsplash.com/random/452x175?winter',
          href: "board/lorem-5",
        },
        {
          topic: 'Lorem 6',
          description: 'lorem ipsum dolar',
          department: 1,
          background: 'https://source.unsplash.com/random/452x176?winter',
          href: "board/lorem-6",
        },
        {
          topic: 'Lorem 7',
          description: 'lorem ipsum dolar',
          department: 1,
          background: 'https://source.unsplash.com/random/452x177?winter',
          href: "board/lorem-7",
        },
        {
          topic: 'Lorem 8',
          description: 'lorem ipsum dolar',
          department: 3,
          background: 'https://source.unsplash.com/random/451x177?winter',
          href: "board/lorem-8",
        },
        {
          topic: 'Lorem 9',
          description: 'lorem ipsum dolar',
          department: 4,
          background: 'https://source.unsplash.com/random/453x175?winter',
          href: "board/lorem-9",
        },
        {
          topic: 'Lorem 10',
          description: 'lorem ipsum dolar',
          department: 3,
          background: 'https://source.unsplash.com/random/453x176?winter',
          href: "board/lorem-10",
        },
      ],
      filteredBoards: [],
      newTopic: '',
      newDescription: '',
      newImage: 'https://source.unsplash.com/random/453x177?winter',
    }
  },
  methods: {
    resetFilter() {
      this.filteredBoards = this.boards;
    },
    addBoard() {
      let newObj = {
        topic: this.newTopic,
        description: this.newDescription,
        department: 1,
        background: this.newImage,
        href: "board/" + this.newTopic.split(' ').join('-'),
      }

      this.newTopic = '';
      this.newDescription = '';
      this.newImage = '';

      document.getElementById('add_form').style.display = "none";

      return this.boards.push(newObj);
    },
    toggleForm() {
      let form = document.getElementById('add_form');
      if(form.style.display != 'none') {
        form.style.display = 'block';
      } else {
        form.style.display = 'none';
      }
    }
  },
  computed: {
    filterBoards(dep) {
      console.log(dep)
      this.boards.forEach(board => {
        if(board.department == dep) {
          this.filteredBoards.push(board);
        }
      });
    },
  },
}
</script>

<style lang="scss">
  .home {
    height: 100vh;
    width: 100%;
    background: #0a2238;

    #boards {
      .board-wrapper {
        width: 100%;
        display: grid;
        gap: 30px;
        grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
        .board {
          height: 175px;
          // background: #ff8a82;
          overflow: hidden;
          transition: all 200ms;
          display: flex;
          text-decoration: none;
          &:hover {
            box-shadow: 1px 1px 10px rgba(255,255,255,1);
            // transform: scale(1.02);
            cursor: pointer;
          }

          .text {
            color: #FFF;
            padding: 15px;
            margin-top: auto;
            width: 100%;
            background: rgba(0,0,0,0.4);
            box-shadow: 1px 1px 10px rgba(0,0,0,0.7);
          }
        }
      }
    }

    .filter {
      display: grid;
      grid-template-columns: repeat(8, 1fr);
      gap: 30px;
      padding: 30px 0;
      color: #FFF;

      .department-filter {
        padding: 15px;
      }
      .btn {
        background: #ff8383;
        font-weight: 600;
        text-align: center;
        transition: all 200ms;
        &:hover {
          background: #c96060;
          cursor: pointer;
        }
      }
    }
    .add-form {
      padding: 15px;
      background: rgba(255,255,255,0.7);
      backdrop-filter: blur(7px);
      border-radius: 5px;
      width: 350px;
      position: fixed;
      top: 10%;
      right: 1%;

      .form-group {
        padding: 10px 0px;

        .form-text {
          width: 100%;
          padding: 5px;
          font-size: 1.2rem;
          border-radius: 5px;
          outline: none;
          border: 0;
          background: rgba(255,255,255,0.7)
        }
      }
      button {
        background: #4ba735;
        outline: none;
        border: 0;
        padding: 7px 25px;
        color: #FFF;
        font-size: 1.2rem;
        transition: all 200ms;
        margin-top: 15px;

        &:hover {
          cursor: pointer;
          opacity: 0.8;
        }
      }
      h3 {
        margin-bottom: 15px;
        text-align: center;
        font-size: 1.5rem;

      }
    }
    #toggle_form {
      background: #F00;
      font-size: 1.8rem;
      width: fit-content;
      padding: 10px 18px;
      color: #FFF;
      font-weight: 700;
      position: fixed;
      bottom: 5%;
      right: 5%;
      border-radius: 25px;
      box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
      transition: all 200ms;
      &:hover {
        opacity: 0.8;
        cursor: pointer;
      }
    }
  }
</style>