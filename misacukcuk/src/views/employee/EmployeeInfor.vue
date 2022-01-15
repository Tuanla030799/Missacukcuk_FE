<template>
  <div
    id="dlgEmployeeDialog"
    class="dialog"
    :class="{ 'dialog-hide': !showDialog }"
  >
    <div class="model"></div>
    <div class="dialog-content">
      <div class="dialog-header">
        <div class="dialog-header-left">
          <div class="dialog-title">Thông tin nhân viên</div>
          <div class="isCustomer">
            <input type="checkbox" />
            <div class="checkbox-title">Là khách hàng</div>
          </div>
          <div class="isCustomer">
            <input type="checkbox" />
            <div class="checkbox-title">Là nhà cung cấp</div>
          </div>
        </div>
        <div class="dialog-header-right">
          <div class="icon-nav icon-question dialog-question-buton"></div>
          <div
            class="icon-nav icon-close dialog-close-button"
            @click="btnHideDialog()"
          ></div>
        </div>
      </div>

      <div class="dialog-body">
        <div class="dialog-body-top">
          <div class="employee-infor infor-left">
            <div class="grid-infor-left">
              <div class="text">Mã ( <span>*</span> )</div>
              <input
                type="text"
                ref="txtEmployeCode"
                class="dialog-input"
                v-model="employee.employeeCode"
              />
            </div>
            <div class="grid-infor-left">
              <div class="text">Tên ( <span>*</span> )</div>
              <input
                type="text"
                id="txtFullName"
                class="dialog-input"
                v-model="employee.fullName"
              />
            </div>
            <div class="grid-infor-left grid-infor-left-3">
              <div class="text">Đơn vị ( <span>*</span> )</div>
              <select
                id="cbEmployeeGroup"
                class="dialog-input"
                v-model="employee.employeeGroupId"
              >
                <option value="19165ed7-212e-21c4-0428-030d4265475f">
                  Phòng hành chính
                </option>
                <option value="3631011e-4559-4ad8-b0ad-cb989f2177da">
                  Phòng nhân sự
                </option>
                <option value="7a0b757e-41eb-4df6-c6f8-494a84b910f4">
                  Phòng IT
                </option>
                <option value="2924c34d-68f1-1d0a-c9c7-6c0aeb6ec302">
                  Phòng đào tạo
                </option>
              </select>
            </div>
            <div class="grid-infor-left grid-infor-left-3">
              <div class="text">Chức danh</div>
              <input
                type="text"
                id="txtEmployeTitle"
                class="dialog-input"
                v-model="employee.positionName"
              />
            </div>
          </div>
          <div class="employee-infor infor-right">
            <div class="grid-infor-right grid-infor-right-1">
              <div class="text">Ngày sinh</div>
              <input
                type="date"
                id="txtEmployeDate"
                class="dialog-input"
                v-model="dateOfBirthFormat"
              />
            </div>
            <div class="grid-infor-right grid-infor-right-2">
              <div class="text-gioitinh">Giới tính</div>
              <div class="dialog-input">
                <input
                  type="radio"
                  id="nam"
                  name="gender"
                  value="1"
                  v-model="employee.gender"
                />
                <label for="nam">Nam</label>
                <input
                  type="radio"
                  id="nu"
                  name="gender"
                  value="0"
                  v-model="employee.gender"
                />
                <label for="nam">Nữ</label>
                <input
                  type="radio"
                  id="khac"
                  name="gender"
                  value="2"
                  v-model="employee.gender"
                />
                <label for="nam">Khác</label>
              </div>
            </div>
            <div class="grid-infor-right grid-infor-right-3">
              <div class="text">Số CMND</div>
              <input
                type="text"
                id="txtCMND"
                class="dialog-input"
                v-model="employee.identityCardNumber"
              />
            </div>
            <div class="grid-infor-right grid-infor-right-4">
              <div class="text">Ngày cấp</div>
              <input
                type="date"
                id="txtCMNDDate"
                class="dialog-input"
                v-model="dateIdentityFornat"
              />
            </div>
            <div class="grid-infor-right grid-infor-right-5">
              <div class="text">Nơi cấp</div>
              <input
                type="text"
                id="txtCMNDPlace"
                class="dialog-input"
                v-model="employee.identityCardPlace"
              />
            </div>
          </div>
        </div>
        <div class="dialog-body-bot">
          <div class="grid-infor-bot grid-infor-bot-1">
            <div class="text">Địa chỉ</div>
            <input
              type="text"
              id="txtAddress"
              class="dialog-input"
              v-model="employee.address"
            />
          </div>
          <div class="grid-infor-bot grid-infor-bot-2">
            <div class="text">ĐT di động</div>
            <input
              type="text"
              id="txtPhoneMobile"
              class="dialog-input"
              v-model="employee.mobilePhoneNumber"
            />
          </div>
          <div class="grid-infor-bot grid-infor-bot-3">
            <div class="text">Đt cố định</div>
            <input
              type="text"
              id="txtPhone"
              class="dialog-input"
              v-model="employee.phoneNumber"
            />
          </div>
          <div class="grid-infor-bot grid-infor-bot-4">
            <div class="text">Email</div>
            <input
              type="text"
              id="txtEmail"
              class="dialog-input"
              v-model="employee.email"
            />
          </div>
          <div class="grid-infor-bot grid-infor-bot-5">
            <div class="text">Tài khoản ngân hàng</div>
            <input
              type="text"
              id="txtBankNumber"
              class="dialog-input"
              v-model="employee.bankCardNumber"
            />
          </div>
          <div class="grid-infor-bot grid-infor-bot-6">
            <div class="text">Tên ngân hàng</div>
            <input
              type="text"
              id="txtBankName"
              class="dialog-input"
              v-model="employee.bankName"
            />
          </div>
          <div class="grid-infor-bot grid-infor-bot-7">
            <div class="text">Chi nhánh</div>
            <input
              type="text"
              id="txtBankBranch"
              class="dialog-input"
              v-model="employee.bankBranch"
            />
          </div>
        </div>
      </div>

      <div class="dialog-footer">
        <div class="dialog-footer-left">
          <button class="button-text btn-destroy" @click="btnHideDialog()">
            Hủy
          </button>
        </div>
        <div class="dialog-footer-right">
          <button class="button-text btn-hide">Cất</button>
          <button class="btn-default btn-hide-and-add" @click="btnSaveClick()">
            Cất và thêm
          </button>
        </div>
      </div>
    </div>
    <employee-noti-error
      :hideNotiError="showNotiError"
      :ErrorMSg="notiError"
      @hideError="hideErrorNoti"
    />
  </div>
</template>

<script>
import axios from "axios";
import EmployeeNotiError from "./EmployeeNotiError.vue";
export default {
  name: "employee-infor",
  components: {
    EmployeeNotiError,
  },
  props: {
    showDialog: {
      type: Boolean,
      default: false,
    },
    employee: {
      type: Object,
    },
    formMode: {
      type: String,
      default: "add",
    },
    //obj check trùng id chính nó update
    employeeUpdate: {
      type: Object,
      default: null,
    },
    //obj check trùng id update
    employeeCheckUpdate: {
      type: Array,
      default: null,
    },
  },
  data() {
    return {
      notiError: "",
      showNotiError: false,
    };
  },
  methods: {
    btnHideDialog() {
      this.$emit("hideDialog");
      console.log(this.employeeUpdate.employeeCode);
    },
    btnSaveClick() {
      //vòng lặp check trùng mã nv nếu trùng tăng index
      var indexEmployee = -1;
      this.employeeCheckUpdate.forEach((e, index) => {
        if (e.employeeCode == this.employee.employeeCode) {
          indexEmployee = index;
         // console.log(this.employee.employeeCode);
        }
      });
      if (this.formMode == "add") {
        axios
          .post("https://localhost:44369/api/v1/Employees", this.employee)
          .then((res) => {
            console.log(res);
            this.notiError = res.devMsg;
            console.log(this.notiError);
            this.$emit("hideDialog");
            this.$emit("addTotal");
          })
          .catch((res) => {
            console.log(res);
            this.notiError = res.response.data.devMsg;
            this.showNotiError = true;
            // console.log(res.response.data.devMsg);
          });
      } else if (this.formMode == "edit") {
        if (this.employee.employeeCode == this.employeeUpdate.employeeCode) {
          // console.log(this.employee.employeeCode);
          //console.log(this.employeeUpdate.employeeCode)
          this.putData();
          
        } else {
          if (indexEmployee != -1) {
            console.log(this.employee.EmployeeCode);
            console.log(this.employeeUpdate.employeeCode);
            this.notiError = "mã nhân viên ${this.employee.employeeCode} đã tồn tại trogn hệ thống vui lòng nhập lại!";
            this.showNotiError = true;
          } else {
            //console.log(this.employee.EmployeeCode);
            //console.log(this.employeeUpdate.employeeCode);
            //this.putData();
            console.log("dit me th ngu")
          }
        }
        //this.putData();
      }
    },

    // hàm put dữ liệu
    putData() {
      axios
        .put(
          "https://localhost:44369/api/v1/Employees/" +
            this.employee.employeeId,
          this.employee
        )
        .then((res) => {
          console.log(res);
          this.$emit("hideDialog");
        })
        .catch((res) => {
          console.log(res);
        });
    },

    //ẩn thông báo lỗi
    hideErrorNoti() {
      this.showNotiError = false;
    },

    /**
     * Hàm chuyển date string về dạng YYYY-MM-DD
     */
    formatDate(dateStr) {
      if (dateStr) {
        let date = new Date(dateStr);
        let dateString =
          date.getDate() < 10
            ? "0" + date.getDate().toString()
            : date.getDate().toString();
        let monthString =
          date.getMonth() < 9
            ? "0" + (date.getMonth() + 1).toString()
            : (date.getMonth() + 1).toString();
        let yearString = date.getFullYear().toString();
        return `${yearString}-${monthString}-${dateString}`;
      }
      return null;
    },
  },
  computed: {
    // format Date
    dateOfBirthFormat: {
      get() {
        return this.formatDate(this.employee.dateOfBirth);
      },
      set(val) {
        this.employee.dateOfBirth = val;
      },
    },
    dateIdentityFornat: {
      get() {
        return this.formatDate(this.employee.identityCardDate);
      },
      set(val) {
        this.employee.identityCardDate = val;
      },
    },
  },
  watch: {
    showDialog: function (val) {
      if (val) {
        this.$nextTick(function () {
          this.$refs.txtEmployeCode.focus();
        });
      }
    },
  },
};
</script>

<style scoped>
.icon-question,
.icon-close {
  width: 24px;
  height: 24x;
  min-width: 24px;
  min-height: 24px;
}
input:focus {
  border: 1px solid #2ca01c !important ;
}
</style>