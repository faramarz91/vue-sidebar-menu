<template>
  <aside :class="`${is_expanded && 'is-expanded'}`">
    <div class="logo">
      <img src="../assets/vue.svg" alt="VUE">
    </div>
    
    <div class="menu-toggle-wrap">
      <button class="menu-toggle" @click="ToggleMenu">
        <span class="material-icons">keyboard_double_arrow_right</span>
      </button>
    </div>
    <h3>Menu</h3>
    <div class="menu">
      <router-link class="button" to="/">
        <span class="material-icons">home</span>
        <span class="menu-item">Home</span>
      </router-link>
      <router-link class="button" to="/about">
        <span class="material-icons">visibility</span>
        <span class="menu-item">About</span>
      </router-link>
      <router-link class="button" to="/team">
        <span class="material-icons">group</span>
        <span class="menu-item">Team</span>
      </router-link>
      <router-link class="button" to="/contact">
        <span class="material-icons">email</span>
        <span class="menu-item">Contatc</span>
      </router-link>
    </div>
    <div class="flex"></div>
    <div class="menu">
      <router-link class="button" to="/settings">
        <span class="material-icons">settings</span>
        <span class="menu-item">Setting</span>
      </router-link>
    </div>
  </aside>
</template>

<script setup>
import { ref } from 'vue';

const is_expanded = ref(localStorage.getItem('is_expanded') === "true");

const ToggleMenu = () => {
  is_expanded.value = !is_expanded.value;
  localStorage.setItem('is_expanded', is_expanded.value)
}

</script>

<style lang="scss" scoped>
  aside {
    display: flex;
    flex-direction: column;
    @media (max-width: 414px) {
      min-height: 100vh;
      margin-block: 0;
    };
    @media (max-height: 400px) {
      min-height: 100vh;
      margin-block: 0;
      h3 {
        display: none;
      }
    }
    height: 90vh;
    margin-block: 5vh;
    width: calc(2rem + 32px);
    overflow: hidden;
    padding: 1rem;

    background-color: var(--dark);
    border-radius: 0 1em 1rem 0;
    box-shadow: 1px 1px 4px 0px var(--gray);
    color: var(--light);

    transition: .3s cubic-bezier(1, -0.5, 0, 1.5);

    .flex {
      flex: 1 1 0;
    }
    .logo {
      margin-bottom: 1rem;
      display: flex;
      justify-content: start;
      animation: logoShakeIn .3s;

      img {
        width: 2rem;
      }
    }

    .menu-toggle-wrap {
      display: flex;
      justify-content: end;
      margin-bottom: 1rem;

      position: relative;
      top: 0;
      transition: .3s cubic-bezier(1, 1, 0, 1);

      .menu-toggle {
        transition: .3s ease-out;
        
        .material-icons {
          transition: .3s ease-out;
          font-size: 2rem;
          color: var(--light);
        }
        &:hover {
          transform: translateX(.3rem);
          .material-icons {
            color: var(--primary);
          }
        }
      }

    }

    h3 {
      color: var(--gray);
      font-size: .857rem;
      text-transform: uppercase;
      padding-bottom: 1rem;
      margin-bottom: 1rem;
      border-bottom: 1px solid var(--dark-alt);
    }

    h3, .button .menu-item {
      opacity: 0;
      transition: .3s ease-out;
    }

    .menu {
       margin: 0 -1rem;

       .button {
        display: flex;
        align-items: center;
        text-decoration: none;

        padding: .5rem 1rem;
        transition: .2s ease-out;

        .material-icons {
          font-size: 2rem;
          color: var(--light);
          transition: .2s ease-out;
          z-index: 10;
          background-color: var(--dark);
        }

        .menu-item {
          color: var(--light);
          margin-left: -3rem;
          transition: .2s ease-out;
          z-index: 1;
        }

        &:hover {
          background-color: var(--dark-alt);

          .material-icons, .menu-item {
            color: var(--primary);
            background-color: var(--dark-alt);
          }
        }

        &.router-link-active, &.router-link-exact-active {

          .material-icons, .menu-item {
            color: var(--primary);
          }
          border-right: .5rem solid var(--primary);
          
        }

       }
    }

    &.is-expanded {
      width: var(--sidebar-width);

      
      .menu-toggle-wrap {
        top: -3rem;
        
        &:hover {
          transform: translateX(- 0.3rem);
        }
        .menu-toggle {
          transform: rotate(180deg);

        }
      }
      .logo {
        display: flex;
        justify-content: start;
        animation: logoShakeOut .3s;
      }

      h3, .button .menu-item {
      opacity: 1;
      }

      .button {
        .menu-item {
          margin-left: 0;
        }
        .material-icons {
          margin-right: 1rem;
        }
      }

    }

    @media (max-width: 768px) {
      position: fixed;
      z-index: 99;
    }

    @keyframes logoShakeIn {
      0% {transform: scale(1);}
      45% {transform: scale(1);margin-left: 0;}
      90% {transform: scale(.8); margin-left: -1.2rem;}
      100% {transform: scale(1);margin-left: 0;}
    }

    @keyframes logoShakeOut {
      0% {transform: scale(1);margin-left: 0;}
      10% {transform: scale(.7); margin-left: -1.2rem;}
      55% {transform: scale(1);margin-left: 0;}
      100% {transform: scale(1);}
    }
  }
</style>