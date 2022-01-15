<template>
  <div class="employee-delete" :class="{ 'dialog-hide': !showDeleteDialog }">
    <div class="model"></div>
    <div class="delete-content">
      <div class="dialog-body">
        <div class="icon-nav dialog-item icon-noti-delete"></div>
        <div class="dialog-text">
          Bạn có chắc chắn muốn xóa nhân viên có mã nhân viên là: {{ employeeDelete.employeeCode }} không?
        </div>
      </div>
      <div class="dialog-footer-delete">
        <div class="btn-dialog">
          <div class="btn-default destroy" @click="btnDestroyDlgDelete()">Không</div>
          <div id="btnSave" class="btn-default btn-commit"
          @click="btnCommitDeleteClick()">Có</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "employee-delete",
  props: {
    showDeleteDialog: {
      type: Boolean,
      default: false
    },
    employeeDelete: {
        type: Object,
        default: null
    }
  },
  methods: {
    btnDestroyDlgDelete() {
      this.$emit('hideDlgDelete')
    },
    btnCommitDeleteClick() {
      axios
          .delete("http://api.manhnv.net/v1/Employees/" + this.employeeDelete.employeeId )
          .then((res)=>{
              console.log(res);
              this.$emit ('hideDeleteDialog')
          })
          .catch((res)=>{
              console.log(res)
          })
    }
  }
};
</script>

<style scoped>
.delete-content {
  padding: 32px;
  position: fixed;
  top: 38%;
  left: 40%;
  width: 380px;
  height: 139px;
  border-radius: 4px;
  background-color: #ffffff;
}
.model {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #000000;
  opacity: 0.4;
}

.dialog-footer-delete {
  position: absolute;
  right: 0px;
  left: 0px;
  bottom: 0px;
  height: 60px;
  
}
.dialog-body {
  top: 32px !important;
  display: flex;
  height: 82px;
  
}
.dialog-body .dialog-item {
  width: 65px;
  height: 48px;
}
.dialog-body .dialog-text {
  margin-top: 5px;
  margin-left: 10px;
  font-weight: 600px !important;
  font-size: 15px !important;
  /* margin-bottom: 64px; */
}
.btn-commit {
  float: right;
}
.destroy {
  background-color: #ffffff;
  color: #000000;
  border: 1px solid #bbb;
}
.destroy:hover {
  background-color: #bbb;
}
.btn-dialog {
  align-items: center;
  justify-content: space-between !important;
  padding:0 32px 0 32px;

}

.icon-noti-delete {
  background-position: -592px -456px!important;
}

</style>