<template>
    <header style="background-color: #1c1c1c; padding-bottom: 10px">
      <div class="navbar">
        <div class="logo"><router-link to="/home">Facial API.com</router-link></div>
        <ul class="links">
          <li><router-link :to="backToDetails">Voltar aos detalhes do Grupo</router-link></li>
          <li><router-link :to="openSessionsLink">Sessões em Andamento</router-link></li>
          <li><router-link :to="accessSessionsLink">Sessões Encerradas</router-link></li>
          <li><router-link :to="createSessionLink">Iniciar Sessão</router-link></li>
        </ul>
        <logout-button class="logout-button"></logout-button>
        <div class="toggle-btn" @click="toggleMenu">
          <i class="fas fa-bars"></i>
        </div>
        <div class="dropdown-menu" :class="{ open: menuOpen }">
          <ul>
            <li><router-link :to="backToDetails">Voltar aos detalhes do Grupo</router-link></li>
            <li><router-link :to="openSessionsLink">Sessões em Andamento</router-link></li>
            <li><router-link :to="accessSessionsLink">Sessões Encerradas</router-link></li>
            <li><router-link :to="createSessionLink">Criar Sessão</router-link></li>
          </ul>
        </div>
      </div>
    </header>
  </template>
  
  <script>
  import LogoutButton from './LogoutButton.vue';
  
  export default {
    name: 'OsNavbar',
    components: {
      'logout-button': LogoutButton
    },
    props: {
      groupName: {
        type: String,
        required: true
      }
    },
    data() {
      return {
        menuOpen: false
      };
    },
    computed: {
      createSessionLink() {
        return `/grupos/${this.groupName}/sessoes/iniciar`;
      },
      accessSessionsLink() {
        return this.groupName ? `/grupos/${this.groupName}/sessoes/encerradas` : '#';
      },
      openSessionsLink() {
        return this.groupName ? `/grupos/${this.groupName}/sessoes/em-andamento` : '#';
      },
      backToDetails() {
        return this.groupName ? `/grupos/${this.groupName}/detalhes` : '#';
      }
    },
    methods: {
      toggleMenu() {
        this.menuOpen = !this.menuOpen;
      },
      goBack() {
        if (this.$router) {
          this.$router.back();
        }
      }
    }
  };
  </script>
  
  <style scoped>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
  }
  
  .back-wrapper {
    margin-bottom: 10px;
    background-color: #1c1c1c;
  }
  
  .new-body {
    background: url('../assets/darkbackground.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    position: relative;
  }
  
  li {
    list-style: none;
  }
  
  a {
    text-decoration: none;
    color: #fff;
    font-size: 1rem;
  }
  
  a:hover {
    color: rgb(0, 98, 255);
  }
  
  /* HEADER */
  header {
    position: relative;
    padding: 0 2rem;
  }
  
  .navbar {
    width: 100%;
    height: 60px;
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  
  .navbar .logo a {
    font-size: 2rem;
    font-weight: bold;
  }
  
  .navbar .links {
    display: flex;
    gap: 2rem;
  }
  
  .navbar .toggle-btn {
    color: #fff;
    font-size: 1.5rem;
    cursor: pointer;
    display: none;
  }
  
  .action-btn {
    background-color: rgb(0, 98, 255);
    color: #fff;
    padding: 0.5rem 1rem;
    border: none;
    outline: none;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: bold;
    cursor: pointer;
    transition: scale 0.2s ease;
  }
  
  .action-btn:hover {
    scale: 1.05;
    color: #fff;
  }
  
  .action-btn:active {
    scale: 0.95;
  }
  
  .dropdown-menu {
    display: none;
    position: absolute;
    right: 2rem;
    top: 60px;
    height: 0;
    width: 300px;
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(15px);
    border-radius: 10px;
    overflow: hidden;
    transition: height 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
  
  .dropdown-menu li {
    padding: 0.7rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .dropdown-menu .open {
    height: 240px;
  }
  
  .dropdown-menu .action-btn {
    width: 100%;
    display: flex;
    justify-content: center;
  }
  
  /* DESIGN RESPONSIVO */
  @media (max-width: 992px) {
    .navbar .links,
    .navbar .action-btn {
      display: none;
    }
  
    .navbar .toggle-btn {
      display: block;
    }
  
    .dropdown-menu {
      display: block;
    }
  }
  
  @media (max-width: 576px) {
    .dropdown-menu {
      left: 2rem;
      width: unset;
    }
  }
  </style>
  