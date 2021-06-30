<template>
  <div class="main">
    <div v-for="(name, key) in this.winners" :key="key">
      {{ key + 1 }} - {{ name }}
    </div>
  </div>
</template>



<script>
import { db } from "../firebase";

export default {
  name: "Ranking",
  data: () => ({
    winners: [],
  }),
  created() {
      console.log('Call created')
      db.collection("winner")
      .orderBy("timestamp")
      .onSnapshot((querySnapshot) => {
        this.winners = [];
        querySnapshot.forEach((doc) => {
          this.winners.push(doc.data().name);
        });
      });
  },
  methods: {},
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
