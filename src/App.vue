<template>
  <div class="container column">

    <app-select-block @blockAdded="addBlock" />
    <app-body-resume :blocks="blocks"/>
  </div>
  <div class="container">
    <AppLoader v-if="loader"/>
    <app-comments
        @loadComments="loadComments"
        :comments="comments"
        :loader="loader"
    />
  </div>




</template>

<script>
import AppSelectBlock from "@/components/AppSelectBlock";
import AppBodyResume from "@/components/AppBodyResume";
import AppComments from "@/components/AppComments";
import AppLoader from "@/components/AppLoader";

import axios from 'axios'


export default {
  data() {
    return {
      blocks: [],
      comments: [],
      loader: false
    }
  },
  components: {
    AppSelectBlock,
    AppBodyResume,
    AppComments,
    AppLoader
  },

  methods: {
    addBlock(block) {
      this.blocks.push(block)
    },
    async loadComments() {
      this.loader = true
      const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
      if (!data){
        throw new Error('Произошла ошибка')
      }else {
        this.comments = data
        this.loader = false
      }

     console.log( typeof this.comments)
    }
  },

}
</script>


<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
