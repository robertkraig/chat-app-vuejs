<template>
  <div id="view" :class="menuClass" v-touch:swipe.left="closeMenu" v-touch:swipe.right="openMenu">
    <div id="app-menu-container">
      <aside>
        <nav id="side-menu">
          <h2>AWS Chat</h2>
          <ul>
            <router-link tag="li" :to="{name: 'Group'}">Group Chat</router-link>
            <router-link @click="restMenuClass()" tag="li" :to="{name: 'Chats'}">My Chats</router-link>
            <router-link tag="li" :to="{name: 'Users'}">Users</router-link>
            <router-link tag="li" :to="{name: 'Invites'}">Invites</router-link>
            <router-link tag="li" :to="{name: 'Settings'}">Settings</router-link>
            <router-link tag="li" to="/signout">Sign Out</router-link>
          </ul>
        </nav>
      </aside>
      <router-view id="main"></router-view>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
  
export default {
  name: 'app',
  computed: {
    ...mapGetters({
      menuClass: 'getMenuClass'
    })
  },
  methods: {
    closeMenu() {
      console.log('closing menu...')
      this.setMenuClass('menu-closed')
    },
    openMenu() {
      this.setMenuClass('menu-open')
    },
    ...mapActions({
      toggleMenuClass: 'toggleMenuClass',
      setMenuClass: 'setMenuClass'
    })
  }
}
</script>
<style lang="scss">
  header + main {
    padding-top: 82px;
  }
  
  aside {
    width: 75vw;
    background-color: #4a4a4a;
    min-height: 100vh;
  }
  #side-menu {
    position: fixed;
    margin: 0;
    top: 0;
    width: 75vw;
    padding: 1em;
    box-sizing: border-box;
    font-size: 1.5em;
    color: #cccccc;
    
    h2 {
      text-align: center;
      font-size: 1.5em;
    }
    
    ul {
      margin-top: 1em;
      margin-left: .25em;
    }
    li {
      display: block;
      margin-bottom: .25em;
      cursor: pointer;
      
      &.router-link-active {
        color: white;
      }
    }
  }
  #view {
    max-width: 100%;
    width: 100vw;
    overflow-x: hidden;
    &.menu-open {
      #app-menu-container {
        position: relative;
        right: 0%;
        animation: scrollLeft .25s ease-in-out;
      } 
    }
    &.menu-closed #app-menu-container {
      position: relative;
      animation: scrollRight .25s ease-in-out;
      right: 75%;
    }
  }
  #app-menu-container {
    width: 175vw;
    display: flex;
    position: relative;
    right: 75%;
  }
  #main {
    width: 100vw;
    position: relative;
  }
  @keyframes scrollRight {
    from { right: 0%; }
    to { right: 75%; }
  }
  @keyframes scrollLeft {
    from { right: 75%; }
    to { right: 0%; }
  }
  
  body {
    background-color: #cccccc;
    min-height: 100vh;
    font-family: 'Open Sans', sans-serif;
    box-sizing: border-box;
    margin: 0;
  }

  h1, h2 {
    font-weight: normal;
    font-family: 'Patua One', cursive;
    color: white;
  }

  h1 {
    font-size: 3em;
    text-align: center;
    padding: 40px 0;
    margin: 0
  }
  
  h3 {
    font-size: 1.5em;
  }

  .padded {
    margin-left: 10%;
    margin-right: 10%;
    width: 80%;
  }
  
  .container {
    margin-left: auto;
    margin-right: auto;
    max-width: 425px;
  }
  
  nav.simple {
    text-align: center;
    margin-top: 2em;
    color: white;
    a {
      color: white;
    }
  }
  
  a {
    color: black;
  }

  input {
    width: 100%;
    background: white;
    font-size: 18px;
    border: none;
    padding: .35em .5em;
    margin-bottom: 1em;
    box-sizing: border-box;
  }
  
  button {
    padding: .35em .5em;
    font-size: 18px;
    font-weight: 600;
    background: white;
    border: 1px solid #cccccc;
    
    &.block {
      width: 80%;
      margin-left: auto;
      margin-right: auto;
      margin-top: 1em;
      display: block;
    }
    
    &.inverted {
      color: white;
      background: black;
      border: 1px solid black;
      
      &[disabled] {
        background: #cccccc;
        border: 1px solid #cccccc;
      }
    }
  }

  ul {
    margin: 0;
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }
  
  @media(min-width: 500px) {
    header + main {
      padding-top: 64px;
    }
    
    #view {
      &.menu-open #app-menu-container {
        position: relative;
        right: 75%;
        animation: none;
      }
      &.menu-closed #app-menu-container {
        position: relative;
        right: 75%;
        animation: none;
      }
    }
  }
</style>
