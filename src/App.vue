<template>
  <h3>CASE 4</h3>
  <table>
    <tr>
      <th>Asset name</th>
      <th>Department</th>
    </tr>
      <tr v-for="info in infoRequired" :key="info.asset">
          <td >{{info.asset}}</td>
          <td>{{info.dept}}</td>
      </tr>
  </table>
  <br>
  <button @click="downloadCSV">Download CSV</button>

</template>

<script>
export default {
  data() {
    return {
      infoRequired: [
        {asset: "Printer", dept: "HR"},
        {asset: "Monitor", dept: "IT"},
        {asset: "Barcode Scanner", dept: "ACCOUNT"},
      ]
    };
  },
  
  methods: {
    downloadCSV() {
      const csvContent = this.convertToCSV(this.infoRequired);
      const blob = new Blob([csvContent], { type: 'text/csv' });
      const url = window.URL.createObjectURL(blob);
      
      const a = document.createElement('a');
      a.href = url;
      a.download = 'data.csv';
      a.click();
      
      window.URL.revokeObjectURL(url);
    },
    convertToCSV(data) {
      const header = 'Asset Name, Department'; // Column names
      const rows = data.map(item => Object.values(item).join(','));
      return `${header}\n${rows.join('\n')}`;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table, td, th {
  border: 1px solid;
  padding-left: 20px;

}

table {
  width: 50%;
  border-collapse: collapse;
  text-align: left;
  height: 170px;
  margin-left: auto;
  margin-right: auto;
}


</style>
