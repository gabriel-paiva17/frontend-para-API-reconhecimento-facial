<template>
  <header style="background-color: #1c1c1c; padding-bottom: 10px">
    <div class="navbar">
      <div class="logo"><router-link to="/home">Facial API.com</router-link></div>
      <ul class="links">
        <li><router-link to="/grupos">Meus Grupos</router-link></li>
        <li><router-link to="/grupos/criar">Criar Grupo</router-link></li>
      </ul>
      <div class="actions">
        <button class="delete-user-btn" @click="confirmDeleteUser">Excluir Usuário</button>
        <logout-button class="logout-button"></logout-button>
      </div>
      <div class="toggle-btn" @click="toggleMenu">
        <i class="fas fa-bars"></i>
      </div>
      <div class="dropdown-menu" :class="{ open: menuOpen }">
        <ul>
          <li><router-link to="/services">Sobre Nós</router-link></li>
          <li><router-link to="/grupos">Meus Grupos</router-link></li>
          <li><router-link to="/grupos/criar">Criar Grupo</router-link></li>
          <li><router-link to="/auth/login" class="action-btn">Meu Perfil</router-link></li>
        </ul>
      </div>
    </div>

    <!-- Modal para confirmação de exclusão do usuário -->
    <div v-if="showModalDeleteUser" class="modal">
      <div class="modal-content">
        <span class="close" @click="closeModalDeleteUser">&times;</span>
        <h3>Ao deletar este usuário, todas suas informações serão perdidas. Deseja mesmo continuar?</h3>
        <div class="modal-buttons">
          <button class="confirm-btn" @click="deleteUser">Sim</button>
          <button class="cancel-btn" @click="closeModalDeleteUser">Não</button>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import LogoutButton from './LogoutButton.vue';
import axios from 'axios';

export default {
  name: 'AppNavbar',
  components: {
    'logout-button': LogoutButton
  },
  data() {
    return {
      menuOpen: false,
      showModalDeleteUser: false
    };
  },
  methods: {
    toggleMenu() {
      this.menuOpen = !this.menuOpen;
    },
    confirmDeleteUser() {
      this.showModalDeleteUser = true;
    },
    closeModalDeleteUser() {
      this.showModalDeleteUser = false;
    },
    deleteUser() {
      axios.delete('/auth/delete')
        .then(response => {
          console.log('Usuário deletado:', response.data);
          this.$router.push({ path: '/auth/login' });
        })
        .catch(error => {
          console.error('Erro ao deletar usuário:', error.response ? error.response.data : error.message);
        });
    }
  }
};
</script>

<style scoped>
@import '../styles/MyGroups.css';

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

.navbar .logo {
  margin-top: -12px; /* Ajuste para subir o logo */
}

.navbar .logo a {
  font-size: 2rem;
  font-weight: bold;
}

.navbar .links {
  display: flex;
  gap: 2rem;
  margin-bottom: 10px;
}

.navbar .actions {
  display: flex;
  align-items: center;
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
  transition: scale 0.2 ease;
}

.action-btn:hover {
  scale: 1.05;
  color: #fff;
}

.action-btn:active {
  scale: 0.95;
}

.delete-user-btn {
  background-color: #ff4d4d;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 3px;
  margin-right: 10px;
  margin-top: 5px; /* Ajuste para abaixar o botão */
}

.logout-button {
  margin-top: 4px; /* Ajuste para abaixar o botão */
  padding: 3px 10px;
}

.delete-user-btn:hover {
  background-color: #cc0000;
}

.dropdown-menu {
  display: none;
  position: absolute;
  right: 2rem;
  top: 60px;
  height: 0;
  width: 300px;
  background: rgba(255, 255, 255, .2);
  backdrop-filter: blur(15px);
  border-radius: 10px;
  overflow: hidden;
  transition: height .2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
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

/*DESIGN RESPONSIVO*/
@media(max-width: 992px) {
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

@media(max-width: 576px) {
  .dropdown-menu {
    left: 2rem;
    width: unset;
  }
}

/* Estilos para o modal */
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0,0,0,0.4);
}

.modal-content {
  background-color: #1c1c1c;
  border: 2px solid rgb(0, 98, 255);
  border-radius: 10px;
  padding: 20px;
  text-align: center;
  width: 60%;
  max-width: 800px;
}

.modal-content h3 {
  color: #fff;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}

.modal-buttons {
  display: flex;
  justify-content: space-around;
}

.confirm-btn, .cancel-btn {
  padding: 10px 25px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin: 20px;
}

.confirm-btn:hover, .cancel-btn:hover {
  background-color: #000;
}

.confirm-btn {
  background-color: #ff4d4d;
}

.cancel-btn {
  background-color: #007bff;
}
</style>
