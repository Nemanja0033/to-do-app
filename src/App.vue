<script >
import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Footer from "./components/Footer.vue";

import ToDoItem from "./model/ToDoItem";
import ToDo from "./model/ToDo";

export default {
  name: "App",
  components: {
    'app-header': Header,
    'app-body': Body,
    'app-footer': Footer
  },
  data() {
    return {
      clickedTab: -1,
      currentRoute: window.location.pathname,
      toDo: new ToDo()
    }
  },
  methods: {
    tabChange(tab) {
      this.clickedTab = tab
    },
    itemAdd(content) {
      //alert(content)
      let item = new ToDoItem(content, new Date())
      this.toDo.add(item)
    }
  },
  computed: {
    activeTab() {
      let tab;
      if (this.clickedTab > -1) {
        return this.clickedTab;
      }
      switch (window.location.pathname) {
        case "/all-items":
          tab = 1;
          break;
        case "/pending-items":
          tab = 2;
          break;
        case "/active-items":
          tab = 3;
          break;
      }
      return tab;
    }
  }
}
</script>

<template>
  <div id="app-container">
    <app-header v-on:tab-change="tabChange" v-bind:tab="activeTab"></app-header>
    <app-body v-bind:tab="activeTab" v-bind:todo="toDo"></app-body>
    <app-footer v-on:item-add="itemAdd"></app-footer>
  </div>
</template>

<style scoped>
#app-container {
  max-width: 490px;
  margin: 0 auto;
  height: 95vh;
  background: white;
  border-radius: 10px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  /* transform: translate(0, -50%); */
  transform: translate(0, 2.5%);
  /*  */
  top: 50%;
  position: relative;
  display: flex;
  flex-direction: column;
}
</style>
