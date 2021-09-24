<template>
  <div>
      <header class="l-header scroll-header" id="header">
          <nav class="nav bd-container">
              <a href="#" class="nav__logo">Tasty</a>

              <div class="nav__menu" id="nav-menu">
                  <ul class="nav__list">
                      <li class="nav__item"><a href="#home" class="nav__link active-link" v-on:click="linkAction">Home</a></li>
                      <li class="nav__item"><a href="#about" class="nav__link" v-on:click="linkAction">About</a></li>
                      <li class="nav__item"><a href="#services" class="nav__link" v-on:click="linkAction">Services</a></li>
                      <li class="nav__item"><a href="#menu" class="nav__link" v-on:click="linkAction">Menu</a></li>
                      <li class="nav__item"><a href="#contact" class="nav__link" v-on:click="linkAction">Contact Us</a></li>
                  </ul>
              </div>
              <div class="nav__toggle" id="nav-toggle" v-on:click="showMenu('nav-toggle','nav-menu')">
                  <i class='bx bx-menu'></i>
              </div>
          </nav>
      </header>
  </div>
</template>

<script>
export default {
    methods:{
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
        linkAction(){
            const navMenu = document.getElementById('nav-menu');
            navMenu.classList.remove('show-menu');
        },
        scrollHeader(){
            const nav = document.getElementById('header');
            if(window.scrollY >= 200)
                nav.classList.add('scroll-header');
            else
                nav.classList.remove('scroll-header');
        },
        scrollActive(){
            const sections = document.querySelectorAll('section[id]');
            const scrollY = window.pageYOffset;
            sections.forEach(current => {
                const sectionHeight = current.offsetHeight;
                const sectionTop = current.offsetTop - 50;

                sectionId = current.getAttribute('id');
                if(scrollY > sectionTop && scrollY <= sectionTop + sectionHeight){
                    document.querySelector('.nav__menu a[href*=' + sectionId + ']').classList.add('active-link')
                }else{
                    document.querySelector('.nav__menu a[href*=' + sectionId + ']').classList.remove('active-link')
                }
            })
        }
    },
    mounted(){
        this.scrollHeader();
        this.scrollActive();
    }
}
</script>

<style>
:root{
    --header-height: 3rem;

  /*========== Colors ==========*/
  --first-color: #069C54;
  --first-color-alt: #048654;
  --title-color: #393939;
  --text-color: #707070;
  --text-color-light: #A6A6A6;
  --body-color: #FBFEFD;
  --container-color: #FFFFFF;

  /*========== Font and typography ==========*/
  --body-font: 'Poppins', sans-serif;
  --biggest-font-size: 2.25rem;
  --h1-font-size: 1.5rem;
  --h2-font-size: 1.25rem;
  --h3-font-size: 1rem;
  --normal-font-size: .938rem;
  --small-font-size: .813rem;
  --smaller-font-size: .75rem;

  /*========== Font weight ==========*/
  --font-medium: 500;
  --font-semi-bold: 600;

  /*========== Margenes ==========*/
  --mb-1: .5rem;
  --mb-2: 1rem;
  --mb-3: 1.5rem;
  --mb-4: 2rem;
  --mb-5: 2.5rem;
  --mb-6: 3rem;

  /*========== z index ==========*/
  --z-tooltip: 10;
  --z-fixed: 100;
}

@media screen and (min-width: 768px){
  :root{
    --biggest-font-size: 4rem;
    --h1-font-size: 2.25rem;
    --h2-font-size: 1.5rem;
    --h3-font-size: 1.25rem;
    --normal-font-size: 1rem;
    --small-font-size: .875rem;
    --smaller-font-size: .813rem;
  }
}

/*========== BASE ==========*/
*,::before,::after{
  box-sizing: border-box;
}

html{
  scroll-behavior: smooth;
}
body{
  margin: var(--header-height) 0 0 0;
  font-family: var(--body-font);
  font-size: var(--normal-font-size);
  background-color: var(--body-color);
  color: var(--text-color);
  line-height: 1.6;
}
h1,h2,h3,p,ul{
  margin: 0;
}
ul{
  padding: 0;
  list-style: none;
}
a{
  text-decoration: none;
}

img{
  max-width: 100%;
  height: auto;
}
/*========== CLASS CSS ==========*/
.section{
  padding: 4rem 0 2rem;
}

.section-title, .section-subtitle{
  text-align: center;
}

.section-title{
  font-size: var(--h1-font-size);
  color: var(--title-color);
  margin-bottom: var(--mb-3);
}

.section-subtitle{
  display: block;
  color: var(--first-color);
  font-weight: var(--font-medium);
  margin-bottom: var(--mb-1);
}
/*========== LAYOUT ==========*/
.bd-container{
  max-width: 960px;
  width: calc(100% - 2rem);
  margin-left: var(--mb-2);
  margin-right: var(--mb-2);
}
.bd-grid{
  display: grid;
  gap: 1.5rem;
}

.l-header{
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: var(--z-fixed);
  background-color: var(--body-color);
}
/*========== NAV ==========*/
.nav{
  max-width: 1024px;
  height: var(--header-height);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media screen and (max-width: 768px){
  .nav__menu{
    position: fixed;
    top: -100%;
    left: 0;
    width: 100%;
    padding: 1.5rem 0 1rem;
    text-align: center;
    background-color: var(--body-color);
    transition: .4s;
    box-shadow: 0 4px 4px rgba(0,0,0,.1);
    border-radius: 0 0 1rem 1rem;
    z-index: var(--z-fixed);
  }
}
.nav__item{
    margin-bottom: var(--mb-2);
}
.nav__link, .nav__logo, .nav__toggle{
    color: var(--text-color);
    font-weight: var(--font-medium);
}

.nav__logo:hover{
  color: var(--first-color);
}

.nav__link{
  transition: .3s;
}

.nav__link:hover{
  color: var(--first-color);
}
.nav__toggle{
  font-size: 1.3rem;
  cursor: pointer;
}

/* Show Menu */
.show-menu{
    top: var(--header-height);
}
/* Active menu */
.active-link{
  color: var(--first-color);
}
/* Change background header */
.scroll-header{
  box-shadow: 0 2px 4px rgba(0,0,0,.1);
}

</style>