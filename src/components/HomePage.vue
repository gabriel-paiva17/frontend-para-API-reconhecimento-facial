<template>
    <div >
        <div class="new-body">
            <header>
                <div class="navbar">
                    <div class="logo"><router-link to="/home">Facial API.com</router-link></div>
                    <router-link to = '/auth/login' class="action-btn">Começar Agora</router-link>
                    <div class="toggle-btn" @click="toggleMenu">
                        <i class="fas fa-bars"></i>
                    </div>
                    <div class="dropdown-menu" :class="{ open: menuOpen }">
                        <ul>
                            <li><router-link to="/">Presença</router-link></li>
                            <li><router-link to="/about">Sobre Nós</router-link></li>
                            <li><router-link to="/services">Serviços</router-link></li>
                            <li><router-link to="/contact">Contato</router-link></li>
                            <li><router-link to="/auth/login" class="action-btn">Começar Agora</router-link></li>
                        </ul>
                    </div>
                </div>
            </header>
  
      <main>
        <section id="hero">
          <h1>Facial API</h1>
          <p>
            Ferramenta simples e rápida para facilitar o processo de presença. Chega de chamadas manuais!
          </p>
        </section>
      </main>

        </div>
   
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        menuOpen: false
      };
    },
    methods: {
      toggleMenu() {
        this.menuOpen = !this.menuOpen;
      }
    }
  };
  </script>
  
  <style scoped>
  @import url('../styles/HomePage.css');
  </style>
  