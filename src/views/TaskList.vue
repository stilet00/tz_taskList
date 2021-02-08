<template>
  <div class="taskList">
    <div class="lds-ellipsis"
    v-if="!this.posts.length"

    ><div></div><div></div><div></div><div></div></div>
    <transition-group tag="ol" name="list" class="bullet" appear>
      <li v-for="item in posts" :key="item.id">
        <h3><i>Task name:</i></h3>
        <p>{{ item.title }}</p>
        <router-link :to="'/tasks/' + item.id"
        title="show task's details"
        >Show more</router-link>
      </li>
    </transition-group>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'TaskList',
  data () {
    return {
      posts: []
    }
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/posts')
        .then(res => {
          this.posts.push(...res.data)
        })
        .catch(err => console.log(err))
  },
  components: {
  },
  methods: {
    getTaskList() {

    },
  }
}
</script>
<style>
ul {
  color: black;
}

.bullet {
  margin-left: 0;
  padding: 0;
  list-style: none;
  counter-reset: li;
}
.bullet li {
  position: relative;
  margin-bottom: 1.5em;
  border: 3px solid #CADFCF;
  padding: 0.6em;
  border-radius: 10px;
  background: #FEFEFE;
  color: #231F20;
  font-family: "Trebuchet MS", "Lucida Sans";
}
.bullet li:before {
  position: absolute;
  top: -0.7em;
  padding-left: 0.4em;
  padding-right: 0.4em;
  font-size: 16px;
  font-weight: bold;
  color: black;
  background: #FEFEFE;
  border-radius: 50%;
  counter-increment: li;
  content: counter(li);
}

/*animation */
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

</style>
