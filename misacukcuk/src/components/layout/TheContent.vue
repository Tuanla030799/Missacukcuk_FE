<template>
  <div>
    <div id="content">
      <!-- <router-view></router-view> -->

      <div class="content-hea">
        <div class="content-title">Nhân Viên</div>
        <div class="content-button-add">
          <button class="btn-default btn-add" @click="btnAddDialog">
            Thêm mới nhân viên
          </button>
        </div>
      </div>
      <div class="content-table">
        <div class="search-employee">
          <div class="employee-search">
            <input
              type="text"
              class="input-search"
              style="width: 220px"
              placeholder="Tìm theo mã, tên nhân viên"
              v-model="FindEmployeeCode"
            />
          </div>
          <div
            class="icon-nav content-icon icon-refresh"
            @click="showLoaderClick()"
          ></div>
        </div>
        <div class="employee-table">
          <div class="grid">
            <table id="tblEmployee" class="table" width="100%" border="0">
              <thead>
                <tr>
                  <th>
                    <input type="checkbox" name="all" value="all" />
                    <span class="checkmark"></span>
                  </th>
                  <th>Mã nhân viên</th>
                  <th>Tên nhân viên</th>
                  <th>Giới tính</th>
                  <th>Ngày sinh</th>
                  <th>Số CMND</th>
                  <th>Chức danh</th>
                  <th>Tên đơn vị</th>
                  <th>Số tài khoản</th>
                  <th>Tên ngân hàng</th>
                  <th>Chi nhánh tài khoản ngân hàng</th>
                  <th>Chức năng</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="employee in employees" :key="employee.employeeId">
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>{{ employee.employeeCode }}</td>
                  <td>{{ employee.fullName }}</td>
                  <td>{{ formatGender(employee.gender) }}</td>
                  <td>{{ formatDateDDMMYYYY(employee.dateOfBirth) }}</td>
                  <td>{{ employee.identityCardNumber }}</td>
                  <td>{{ employee.positionName }}</td>
                  <td>{{ formatPositionName(employee.employeeGroupId) }}</td>
                  <td>{{ employee.bankCardNumber }}</td>
                  <td>{{ employee.bankName }}</td>
                  <td>{{ employee.bankBranch }}</td>
                  <td>
                    <div class="Edit">
                      <div class="btn-edit">
                        <button
                          class="button-text button-table-text"
                          @click="btnEditClick(employee.employeeId)"
                        >
                          Sửa
                        </button>
                        <div
                          class="icon-nav arrow-icon icon-arrow-up"
                          @click="showEditClick(employee.employeeId)"
                        ></div>
                      </div>
                      <div
                        class="editDialog"
                        :class="{
                          'dialog-hide': !checkEdit(employee.employeeId),
                        }"
                      >
                        <div class="dialogEdit">
                          <button class="btn-edittable btn-mul">
                            Nhân bản
                          </button>
                          <button
                            class="btn-edittable btn-delete"
                            @click="btnDeleteCode()"
                          >
                            Xóa
                          </button>
                          <button class="btn-edittable btn-use">
                            Ngừng sử dụng
                          </button>
                        </div>
                      </div>
                    </div>
                  </td>

                  <!-- <td>{{ checkEdit(employee.employeeId) }}</td> -->
                </tr>
                <!-- <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr> -->
                <!--  <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr>
                <tr>
                  <td><input type="checkbox" name="all" value="all" /></td>
                  <td>MH-001</td>
                  <td>Lê Anh Tuấn</td>
                  <td>Nam</td>
                  <td>20/05/1999</td>
                  <td>038099004021</td>
                  <td>Giám đốc</td>
                  <td>62pm3</td>
                  <td>9704151300235083</td>
                  <td>Ha Nội</td>
                  <td>Ha Nội</td>
                  <td>Giám đốc</td>
                </tr> -->
              </tbody>
            </table>
          </div>
        </div>
        <div class="paging">
          <div class="page">
            <div class="paging-text">Tổng số: {{ totalRecord }} bản ghi</div>
            <div class="paging-table">
              <select
                name="div-page"
                id="div-page"
                @change="onChangePageSize($event)"
              >
                <option value="20">20 bản ghi trên 1 trang</option>
                <option value="30">30 bản ghi trên 1 trang</option>
                <option value="50">50 bản ghi trên 1 trang</option>
                <option value="100">100 bản ghi trên 1 trang</option>
              </select>
              <button class="btn-text" @click="onClickBackSize()">Trước</button>
              <button class="btn-text" @click="onClickUpSize()">Sau</button>
            </div>
          </div>
        </div>
      </div>
      <loader :isShowLoader="ShowLoader" />
      <employee-infor
        :showDialog="showDetailDialog"
        :employee="SelectedEmployee"
        :formMode="dialogFormMode"
        @hideDialog="hideDialogDetail"
        @addTotal="addTotalInsert"
        :employeeUpdate="CheckEmployeeCode"
        :employeeCheckUpdate="AllData"
      />
      <employee-delete
        :showDeleteDialog="showDetailDeleteDialog"
        :employeeDelete="selectedEmployeeDelete"
        @hideDlgDelete="hideDeleteDlg"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import EmployeeInfor from "../../views/employee/EmployeeInfor.vue";
import EmployeeDelete from "../../views/employee/EmployeeDelete.vue";
import Loader from "../../views/Loader.vue";
export default {
  name: "the-content",
  created() {
    this.getData();
    this.showLoad();
    this.CheckEmployeeCode;
  },
  data() {
    return {
      showDetailDialog: false,
      showDetailDeleteDialog: false,
      ShowLoader: false,
      showEdit: false,
      employees: [],
      SelectedEmployee: {},
      selectedEmployeeDelete: {},
      dialogFormMode: "add",
      selectedId: "",
      FindEmployeeCode: "",
      pageSize: 20,
      pageIndex: 1,
      totalRecord: 20,
      //lấy dữ liệu tính số bản ghi
      datas: [],
      // lấy tất cả giữ liệu
      AllData: [],
      // lấy ra check trùng 
      CheckEmployeeCode: {},
    };
  },
  components: {
    EmployeeInfor,
    Loader,
    EmployeeDelete,
  },

  methods: {
    loadData() {
      var url = `https://localhost:44369/api/v1/Employees`;
      if (this.FindEmployeeCode) {
        url += `/Fillter/divPage?FindAll=${this.FindEmployeeCode}&pageSize=${this.pageSize}&pageIndex=${this.pageIndex}`;
        axios
          .get(url)
          .then((res) => {
            //   console.log(res);
            this.employees = res.data;
            // this.totalRecord = this.employees.length;
          })
          .catch((res) => {
            console.log(res);
          });
      } else {
        url += `/Paging?pageIndex=${this.pageIndex}&pageSize=${this.pageSize}`;
        axios
          .get(url)
          .then((res) => {
            //  console.log(res);
            this.employees = res.data;
            //  this.totalRecord = this.employees.length;
          })
          .catch((res) => {
            console.log(res);
          });
      }
    },

    showLoad() {
      setTimeout(() => {
        this.ShowLoader = true;
        setTimeout(() => this.redirect(), 500);
      });
    },

    redirect() {
      this.ShowLoader = false;
      this.loadData();
    },

    btnAddDialog() {
      this.SelectedEmployee = {
        employeeCode: "",
        fullName: "",
        employeeGroupId: "15fb79ad-271b-30eb-8f32-6a1673ffca7c",
      };
      this.showDetailDialog = true;
    },
    hideDialogDetail() {
      this.showDetailDialog = false;
      this.showLoad();
    },
    showLoaderClick() {
      this.showLoad();
    },
    showEditClick(employeeId) {
      // this.showEdit = !this.showEdit;
      // console.log(this.showEdit)
      this.selectedId = employeeId;
      this.showEdit = !this.showEdit;
    },
    checkEdit(id) {
      // console.log(`${id}   ${this.selectedId}`)
      if (id == this.selectedId) {
        return this.showEdit;
      }
    },
    btnDeleteCode() {
      axios
        .get("https://localhost:44369/api/v1/Employees/" + this.selectedId)
        .then((res) => {
          console.log(res);
          this.selectedEmployeeDelete = res.data;
          this.showDetailDeleteDialog = true;
        })
        .catch((res) => {
          console.log(res);
        });
    },

    hideDeleteDlg() {
      this.selectedId = "";
      this.showDetailDeleteDialog = false;
      this.showLoad();
    },

    btnEditClick(employeeId) {
      axios
        .get("https://localhost:44369/api/v1/Employees/" + employeeId)
        .then((res) => {
          console.log(res);
          this.SelectedEmployee = res.data;
          this.CheckEmployeeCode = res.data;
          console.log(this.CheckEmployeeCode.employeeCode);
        })
        .catch((res) => {
          console.log(res);
        });
      //cap nhap trang thai from
      this.dialogFormMode = "edit";
      this.showLoad();
      this.showDetailDialog = true;
    },
    //lấy value pageSize
    onChangePageSize(event) {
      this.pageSize = event.target.value;
      this.showLoad();
    },
    // PageSize
    onClickBackSize() {
      if (this.pageIndex == 1) {
        this.pageIndex = 1;
        this.showLoad();
      } else {
        this.pageIndex--;
        this.showLoad();
      }
    },
    onClickUpSize() {
      var num = Math.floor(this.totalRecord / this.pageSize);
      if (this.pageIndex == num+1) {
        this.pageIndex = num+1;
        console.log(num);
      } else {
        this.pageIndex++;
        this.showLoad();
      }
    },

    //lay total phan trang
    getData() {
      if (this.FindEmployeeCode) {
        axios
          .get(
            `https://localhost:44369/api/v1/Employees/Fillter/TotalPage?Find=${this.FindEmployeeCode}`
          )
          .then((res) => {
            //console.log(res);
            this.datas = res.data;
            this.totalRecord = this.datas.length;
            this.showLoad();
          })
          .catch((res) => {
            console.log(res);
          });
      } else {
        this.getAllData();
      }
    },


    //lấy toàn bộ dữu liệu
    getAllData() {
      axios
          .get("https://localhost:44369/api/v1/Employees")
          .then((res) => {
            console.log(res);
            this.datas = res.data;
            this.AllData = res.data;
            this.totalRecord = this.datas.length;
            this.showLoad();
          })
          .catch((res) => {
            console.log(res);
          });
    },

    //mỗi lần insert thành công tăng tăng số bản ghi lên 1
    addTotalInsert() {
      this.totalRecord++;
    },

    //xu li ngay thang
    formatDateDDMMYYYY(date) {
      if (!date) {
        return "";
      }
      var newDate = new Date(date);
      var dateString = newDate.getDate();
      var monthString = newDate.getMonth() + 1;
      var year = newDate.getFullYear();
      return `${dateString}/${monthString}/${year}`;
    },
    // ham xu li gioi tinh
    formatGender(gender) {
      if (gender == 0) {
        return "Nữ";
      } else if (gender == 1) {
        return "Nam";
      } else if (gender == 1) {
        return "khác";
      } else {
        return "";
      }
    },
    //xu li chuc danh
    formatPositionName(p) {
      if (p == "19165ed7-212e-21c4-0428-030d4265475f") {
        return "Phòng hành chính";
      } else if (p == "2924c34d-68f1-1d0a-c9c7-6c0aeb6ec302") {
        return "Phòng đào tạo";
      } else if (p == "7a0b757e-41eb-4df6-c6f8-494a84b910f4") {
        return "Phòng IT";
      } else if (p == "3631011e-4559-4ad8-b0ad-cb989f2177da") {
        return "Phòng nhân sự";
      } else {
        return "";
      }
    },
  },
  computed: {
    // SumEmployee: function() {
    // //  var count = 0;
    // //  employees.forEach(element => {
    // //    if (element.employeeId == this.employees.employeeId){
    // //      return count++;
    // //    }
    // //  });
    // return this.pageSize;
    // }
  },
  watch: {
    FindEmployeeCode: function () {
      this.loadData();
      this.getData();
    },
  },
};
</script>

<style scoped>
@import "../../style/layout/content.css";
</style>>
