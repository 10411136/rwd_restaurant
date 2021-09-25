<template>
  <div>
    <header class="l-header" id="header">
        <nav class="nav bd-container">
            <a href="#" class="nav__logo">Tasty</a>

            <div class="nav__menu" id="nav-menu">
                <ul class="nav__list">
                    <!-- <li class="nav__item"><a href="#home" class="nav__link active-link" v-on:click="linkAction">Home</a></li>
                    <li class="nav__item"><a href="#about" class="nav__link" v-on:click="linkAction">About</a></li>
                    <li class="nav__item"><a href="#services" class="nav__link" v-on:click="linkAction">Services</a></li>
                    <li class="nav__item"><a href="#menu" class="nav__link" v-on:click="linkAction">Menu</a></li>
                    <li class="nav__item"><a href="#contact" class="nav__link" v-on:click="linkAction">Contact Us</a></li> -->
                    <li><i class='bx bx-moon change-theme' id="theme-button" v-on:click="changeTheme"></i></li>
                </ul>
            </div>
            <div class="nav__toggle" id="nav-toggle" v-on:click="showMenu('nav-toggle','nav-menu')">
                <i class='bx bx-menu'></i>
            </div>
        </nav>
    </header>
    <main class="l-main">
        <!--========== HOME ==========-->
        <section class="home" id="home">
          <div class="home__container bd-container bd-grid">
            <div v-if="error.statusCode === 404" class="home__data">
              <h1 class="home__title">Page not found</h1>
              <h2 class="home__subtitle">Go back to homepage.</h2>
              <NuxtLink class="button" to="/">Home page</NuxtLink>
            </div>
            <div v-else class="home__data">
                <h1 class="home__title">An error occurred</h1>
            </div>
          </div>
        </section>
    </main>
  </div>
</template>

<script>
  export default {
    props: ['error'],
    layout: 'error', // you can set a custom layout for the error page
    data(){
      return{
        darkTheme: 'dark-theme',
        iconTheme: 'bx-sun'
      }
    },
    methods: {
        /*==================== SHOW MENU ====================*/
        showMenu(toggleId, navId){
            // console.log('1=>',toggleId, navId);
            const toggle = document.getElementById(toggleId),
            nav = document.getElementById(navId);
            // console.log('2=>',toggle, nav);
            // Validate that variables exist
            if(toggle && nav){
                // We add the show-menu class to the div tag with the nav__menu class
                nav.classList.toggle('show-menu');
            }
        },
        changeTheme(){
          document.body.classList.toggle(this.darkTheme);
          document.getElementById('theme-button').classList.toggle(this.iconTheme);
          localStorage.setItem('selected-theme', this.getCurrentTheme());
          localStorage.setItem('selected-icon', this.getCurrentIcon());
        },
        getCurrentTheme(){
          return document.body.classList.contains(this.darkTheme) ? 'dark' : 'light';
        },
        getCurrentIcon(){
          return document.getElementById('theme-button').classList.contains(this.iconTheme) ? 'bx-moon' : 'bx-sun';
        }
    },
    mounted(){
        const selectedTheme = localStorage.getItem('selected-theme');
        const selectedIcon = localStorage.getItem('selected-icon');

        // const getCurrentTheme = () => document.body.classList.contains(this.darkTheme) ? 'dark' : 'light';
        // const getCurrentIcon = () => document.getElementById('theme-button').classList.contains(this.iconTheme) ? 'bx-moon' : 'bx-sun';

        if(selectedTheme){
          document.body.classList[selectedTheme === 'dark'?'add':'remove'](this.darkTheme);
          document.getElementById('theme-button').classList[selectedIcon === 'bx-moon'?'add':'remove'](this.iconTheme);
        }
    }
  }
</script>