<template>
  <div class="mail-list">
    <div class="filters">
      <el-select v-model="filterReadStatus" placeholder="Mail status">
        <el-option label="All" value=""></el-option>
        <el-option label="Read" value="true"></el-option>
        <el-option label="Unread" value="false"></el-option>
      </el-select>
      <el-input
      class="sender-filter"
        v-model="filterSender"
        placeholder="Filter sender"
        clearable
      ></el-input>
    </div>

    <el-table
      :data="filteredRecords"
      ref="multipleTable"
      style="width: 100%"
      @selection-change="handleSelectionChange"
      :row-class-name="readStatus"
      @row-click="openMail"
    >
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column prop="senderName" label="Sender" width="120"></el-table-column>
      <el-table-column prop="subject" label="Subject" width="200"></el-table-column>
      <el-table-column prop="body" label="Preview" min-width="300"></el-table-column>
      <el-table-column prop="time" label="Time" width="150"></el-table-column>
      <el-table-column prop="read" label="Read" width="80">
        <template slot-scope="scope">
          <i class="el-icon-folder-opened" v-if="scope.row.read"></i>
          <i class="el-icon-message" v-else></i>
        </template>
      </el-table-column>
    </el-table>

    <el-dialog v-if="selectedMail" :title="selectedMail.subject" :visible.sync="openModal" width="50%">
      <div class="sender-info">
        <h3>{{ selectedMail.senderName }}</h3>
        <h5>[{{selectedMail.senderEmail}}]</h5>
      </div>
      <p>{{ selectedMail.body }}</p>
      <div class="mail-time">
        <h6>{{ selectedMail.time }}</h6>
      </div>
    </el-dialog>

  </div>
</template>
  
<script>
  import records from '@/assets/records.json';
  
  export default {
    data() {
      return {
        records,
        filterReadStatus: '',
        filterSender: '',
        selectedMail: null,
        openModal:false,
      };
    },
    computed: {
      filteredRecords() {
        return this.records.filter(record =>
          (!this.filterReadStatus || record.read === (this.filterReadStatus === 'true')) &&
          (!this.filterSender || record.senderName.toLowerCase().includes(this.filterSender.toLowerCase()))
        );
      },
    },
    methods: {
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },
      toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {
          this.$refs.multipleTable.clearSelection();
        }
      },
      readStatus ({ row }) {
        return row.read ? 'read-item' : 'unread-item'
      },
      openMail(row) {
        this.selectedMail = row;
        this.openModal = true;
      }
    },
  };
</script>
  
<style>
  .el-table__row.unread-item {
    color: #4b4949;
    font-weight: 600;
    background: #fcf6f6;
  }
  .mail-list {
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  }
  
  .filters {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }

  .sender-filter {
    max-width: 300px;
    margin-right: 30px;
  }
    .el-icon-message {
        color: #000;
        font-size: 20px;
  }
  .el-icon-folder-opened {
    font-size: 20px;
}

.el-dialog__body {
  padding-top: 0px;
  padding-bottom: 5px;
  color: #000;
}

.sender-info {
  display: flex;
  align-items: center;
  margin: 2px 10px;
}

.mail-time {
  display: flex;
  justify-content: flex-end;
}

.mail-time > h6{
  font-size: 12px;
}

.sender-info > h3  {
  margin-right: 10px;
}
  @media (max-width: 750px) {
    .filters {
      flex-direction: column;
    }
  }
</style>
  

  