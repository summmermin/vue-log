<template>
  <div class="main">
    <div>
      <div>
        <form>
          <h1>checkbox</h1>
          <label><input type="checkbox"> ko</label>
          <label><input type="checkbox"> ch</label>
          <label><input type="checkbox"> en</label>
          <p><input type="submit" value="Submit"> <input type="reset" value="Reset"></p>
        </form>
        <hr/>
        <input class="txt" type="text" placeholder="text를 적으세요">
        <button v-on:click="postSummer()">클릭</button>
      </div>
    </div>

    <div>
      <div class="content" v-html="content"></div>
    </div>
  </div>
</template>
<script setup lang="ts">
import axios from "axios";
import {ref} from "vue";

const content = ref('')

const param = {
  domain_id: "love",
  channel_id: 0,
  in_type: "query",
  in_str: "안녕",
  parameters: {
    user_id: "test",
    device_type: "pc",
    lang: "ko",
    raw_str: ""
  },
  session_id: "test",
  dialogue_id: "none",
  log_level: "0"
}

function postSummer() {
  axios.post('http://localhost:3030', param).then((res) => {
    console.log(res)
    content.value += res.headers+`<br/>`
    content.value += res.request.response
  }).catch((err) => {
    console.log(err)
  })
}
</script>
<style>
.content{
  background: darkblue;
}
</style>