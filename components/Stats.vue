<template>
  <div>
    <h3>Base Stats</h3>
    <div class="stats">
      <table width="100%">
        <tr v-for="stat in stats.slice().reverse()">
          <th> {{(stat.stat.name).toUpperCase()}}</th>
          <td class="base_stat"> {{ stat.base_stat }}</td>
          <td>
              <div class="bar" :style="{ width: Math.round((stat.base_stat/255)*100) + '%' }"></div>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

      <!-- <div v-for="stat in stats.slice().reverse()" class="stat">
        {{stat.stat.name}}
        <div class="full"></div>
        <div class="bar" :style="{ width: Math.round((stat.base_stat/255)*100) + '%' }"></div>
      </div> -->

<script>
export default {
  props: ["stats"],
  computed: {
    getGraph: function() {
      return this.stat;
    }
  }
};
</script>

<style scoped>
.stats {
  width: 100%;
  margin-bottom: 7rem;
  
}
.bar {
  background-color: #ffeb3b;
  border-radius: 1rem;
  padding-top: 4px;
  padding-bottom: 4px;
  border: solid #c8bd65 2px;
}

tr:first-child>td:nth-child(3)>div{
  background-color: #4caf50;
  border: solid #337735 2px;
}



h3{
    margin-bottom: 1rem;
    margin-top: 1rem;
}

table { 
    border-collapse: collapse;
}
tr { 
    border-top: solid thin #CFD8DC;
    border-bottom: solid thin #CFD8DC;
}

th, td {
  padding: 5px;
  padding-top: 10px;
  padding-bottom: 10px;
  text-align: left;
}
th{
    width: 20%;
}

.base_stat{
    width: 10%;
}
</style>