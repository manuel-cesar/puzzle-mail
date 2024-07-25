<template>
  <div 
    class="side-menu" 
  >
    <div class="toggle-container">
      <el-switch v-model="isCollapse" active-color="#b0abab" inactive-color="#ff4949"></el-switch>
    </div>
    <el-menu
      :default-active="activeItem"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
      :collapse="isCollapse"
    >  
      <el-menu-item index="inbox"><i class="el-icon-message"></i> <span v-if="!localCollapsed">Inbox</span></el-menu-item>
      <el-menu-item index="sent"><i class="el-icon-circle-close"></i> <span v-if="!localCollapsed">Sent</span></el-menu-item>
      <el-menu-item index="drafts"><i class="el-icon-edit-outline"></i> <span v-if="!localCollapsed">Drafts</span></el-menu-item>
      <el-menu-item index="spam">  <i class="el-icon-warning"></i><span v-if="!localCollapsed">Spam</span></el-menu-item>  
      <el-menu-item index="trash"><i class="el-icon-delete"></i> <span v-if="!localCollapsed">Trash</span></el-menu-item>
      <el-submenu index="labels">
        <template slot="title"><i class="el-icon-folder"></i><span v-if="!localCollapsed">Labels</span></template>
        <el-menu-item index="label-1">Office</el-menu-item>
        <el-menu-item index="label-2">Puzzle</el-menu-item>
        <el-menu-item index="label-3">Personal</el-menu-item>
      </el-submenu>
    </el-menu>
  </div>
</template>


<script>
export default {
  data() {
    return {
      isCollapse: false,
      activeItem: 'inbox'
    };
  },
  methods: {
    handleOpen() {
      console.log('Menu opened');
    },
    handleClose() {
      console.log('Menu closed');
    }
  }
}
</script>


<style scoped>
.side-menu {
  height: 100%;
  background-color: #f5f5f5;
  transition: width 0.5s ease;
}

.toggle-container {
  padding: 10px;
  text-align: center;
}

.el-menu-item.is-active {
  color: #fff;
  background-color: #d8491de0;
}

.el-menu-item:hover {
  color: #303133;
  background-color: #c2975f7c;
}
</style>
