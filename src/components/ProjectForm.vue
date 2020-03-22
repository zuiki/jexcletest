<template lang="html">
 
  <div class="wrapper-jexcel">
    <div class="introduction"><span>Project Feature Sheet</span></div>
    
    <input
      type="button"
      value="Add new row"
      @click="jExcelObj.insertRow()"
    /><br />
    <input
      type="button"
      value="Get value"
      @click="this.insertRowc()"
    /><br />
    <button v-on:click="updateDb">Update</button><br />
    <div id="spreadsheet" ref="spreadsheet"></div>
    <h4>newdata:{{temp}} <br> </h4>
  </div>
</template>

<script>
import jexcelStyle from "jexcel/dist/jexcel.css"; // eslint-disable-line no-unused-vars
import jexcel from "jexcel"; // eslint-disable-line no-unused-vars

export default {
  name: "jexcel",
  data() {
    return {
      temp: "none",
      features: [
        ["SoC", "-", "SoC", "", "modelname", "型番", "Z7213"],
        ["映像出力", "-", "Disp_out:0", "", "comment", "要約", ""],
        ["", "-", "Disp_out:0", "", "resolution", "解像度", ""],
        ["", "-", "Disp_out:0", "", "vsync_rate", "表示更新レート", ""],
        ["", "-", "Disp_out:0", "", "soc_if", "SoCインターフェース", ""],
        ["", "-", "Disp_out:0", "", "boot_init", "ブート時出力", ""],
        ["", "変換IC", "Disp_out:0", "device", "soc_if", "要約", ""],
        ["", "-", "Disp_out:0", "device", "soc_if", "型番", ""]
      ]
    };
  },
  computed: {
    jExcelOptions() {
      console.log(this.features);
      return {
        data: this.features,
        columns: [
          { type: "text", title: "Module", width: "120px" },
          { type: "text", title: "SubModule", width: "120px" },
          { type: "hidden", title: "feamod_main", width: "100px" },
          { type: "hidden", title: "feamod_sub", width: "100px" },
          {
            type: "hidden",
            title: "feamod_member",
            width: "100px"
          },
          { type: "text", title: "Item", width: "180px" },
          { type: "text", title: "Entry", width: "100px" }
        ]
      };
    },
    newdata() {
      var value = "aa";
      //value = yourTableInstance.getData();
      if (this.jExcelObj !== undefined) {
        value = this.jExcelObj.getData();
      }
      //value = this.jExcelObj.getData();
      //value = this.getDate();
      return value;
    }
  },
  methods: {
    insertRowc() {
      console.log(this);
      //this.spreadsheet.insertRow();
    },
    updateDb() {
      console.log(`====: ${JSON.stringify(this.jExcelObj.getJson(), null, 2)}`);
      //console.log(`====${JSON.stringify(this.jExcelObj)}`);
      //return "bbb";
      //return this.jExcelObj.getData();
      this.temp = JSON.stringify(this.jExcelObj.getJson());
    }
  },
  mounted: function() {
    //console.log(this.jExcelOptions);
    //console.log(this.$refs["spreadsheet"]);
    const jExcelObj = jexcel(this.$refs["spreadsheet"], this.jExcelOptions);
    // Object.assign(this, jExcelObj); // pollutes component instance
    Object.assign(this, { jExcelObj }); // tucks all methods under jExcelObj object in component instance
    //console.log(this.jExcelObj);
  }
};
</script>

<style lang="css" scoped>
.introduction {
  font-size: 14px;
  padding: 0.5em;
  margin-bottom: 0.3em;
  color: gold;
  background: #111;
}
</style>
