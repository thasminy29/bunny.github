<template>
  <div id="app" style="font-family: Arial, sans-serif; text-align: center; margin: 0; height: 100vh; display: flex; align-items: center; justify-content: center; background-color: #f3e5f5;">
    <div>
      <h1 style="font-size: 24px; margin-bottom: 20px; color: #333;">Asset Manager</h1>
      <table style="margin: 0 auto; border-collapse: collapse; width: 80vw; max-width: 1200px; border: 1px solid #ddd; background-color: #ffffff;">
        <thead>
          <tr style="background-color: #9b59b6; color: #ffffff;">
            <th style="padding: 12px; border: 1px solid #ddd;">Asset Name</th>
            <th style="padding: 12px; border: 1px solid #ddd;">Department</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in assets" :key="index">
            <td style="padding: 12px; border: 1px solid #ddd;">{{ item.name }}</td>
            <td style="padding: 12px; border: 1px solid #ddd;">{{ item.department }}</td>
          </tr>
        </tbody>
      </table>
      <button @click="downloadCSV" style="margin-top: 20px; padding: 10px 20px; font-size: 16px; cursor: pointer; background-color: #6a1b9a; color: white; border: none; border-radius: 4px;">Download CSV</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      assets: [
        { name: "Printer", department: "HR" },
        { name: "Monitor", department: "IT" },
        { name: "Barcode Scanner", department: "ACCOUNT" }
      ]
    };
  },
  methods: {
    downloadCSV() {
      const headers = "Asset Name,Department\n"; // Add headers here
      const rows = this.assets.map(e => `${e.name},${e.department}`).join("\n");
      const csvContent = "data:text/csv;charset=utf-8," + headers + rows;
      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", "assets.csv");
      document.body.appendChild(link); // Required for FF
      link.click();
    }
  }
};
</script>
