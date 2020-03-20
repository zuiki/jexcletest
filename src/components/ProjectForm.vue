<template lang="html">
  <div class="wrapper-jexcel">
    <div class="introduction"><span>This is a list of my cars</span></div>
    <input
      type="button"
      value="Add new row"
      @click="jExcelObj.insertRow()"
    /><br />
    <div id="spreadsheet" ref="spreadsheet"></div>
  </div>
</template>


