<template>
  <div>
    <div class="lds-ellipsis"
         v-if="!this.singleTask"

    ><div></div><div></div><div></div><div></div></div>
    <transition name="appear-from-right" appear>
      <div class="task-container">
        <h3><i>Task name:</i></h3>
        <p><b>{{singleTask.title}}</b></p>
        <h2><i>What exactly to do:</i></h2>
        <p>{{singleTask.body}}</p>
      </div>
    </transition>

    <router-link to="/" class="back-link">Back to task list</router-link>
  </div>


</template>

<script>

import axios from "axios";

export default {
  name: 'SingleTask',
  data() {
    return {
      singleTask: null
    }
  },
  props: ['page'],
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/posts/' + this.page)
        .then(res => {
          this.singleTask = res.data
        })
        .catch(err => console.log(err))
  }
}
</script>
<style>
.task-container {
  text-align: left;
  position: relative;
  margin-bottom: 1.5em;
  border: 3px solid #CADFCF;
  padding: 0.6em;
  border-radius: 10px;
  background: #FEFEFE;
  color: #231F20;
  font-family: "Trebuchet MS", "Lucida Sans";
}

/*animation of list appearing*/
.appear-from-right-enter, .appear-from-right-enter-fade-to {
  transform: translateX(200px);
  opacity: 0;
}
.appear-from-right-enter-active, .appear-from-right-fade-active {
  transition: all 1s ease-in;
}
</style>
