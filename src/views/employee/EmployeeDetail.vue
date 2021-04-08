<template>
  <div>
    <div
      id="dlgEmployeeDetail"
      class="dialog"
      :class="{ 'dialog-hide': isHide }"
    >
      <div class="model"></div>
      <div class="dialog-content">
        <div class="dialog-header">
          <div class="dialog-title">THÔNG TIN NhÂN VIÊN</div>
          <div class="dialog-close-button" @click="btnCloseOnClick()">
            &#x2715;
          </div>
        </div>
        <div class="dialog-body">
          <div class="body-left">
            <div class="select-image"></div>
            <p>(Vui lòng chọn ảnh có định</p>
            <p>dạng</p>
            <p>.jpg, .jpeg, .png, .gif.)</p>
          </div>
          <div class="body-right">
            <div class="body-title">
              <div class="title-text">A. THÔNG TIN CHUNG:</div>
              <div class="title-container"></div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Mã nhân viên (<span>*</span>)</label>
                <input
                  ref="text-some-input"
                  :value="
                    formMode == 'add' ? newEmployeeCode : employee.EmployeeCode
                  "
                  id="txtEmployeeCode"
                  type="text"
                />
                <span class="mes">{{ validateEmployeeCode }}</span>
              </div>
              <div class="m-col">
                <label>Họ và tên (<span>*</span>)</label>
                <input
                  id="txtFullName"
                  type="text"
                  :value="formMode == 'add' ? '' : employee.FullName"
                />
                <span class="mes">{{ validateFullName }}</span>
              </div>
            </div>
            <div class="m-row" style="margin-bottom: 16px">
              <div class="m-col">
                <label>Ngày sinh</label>
                <input
                  id="dtDateOfBirth"
                  type="date"
                  :value="formMode == 'add' ? '' : dateOfBirth"
                />
              </div>
              <div class="m-col">
                <label>Giới tính</label>
                <select
                  id="cbGender"
                  :value="formMode == 'add' ? '' : employee.Gender"
                >
                  <option value="1">Nam</option>
                  <option value="0">Nữ</option>
                  <option value="2">Không xác định</option>
                </select>
              </div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Số CMTND/ Căn cước (<span>*</span>)</label>
                <input
                  id="txtIdentityNumber"
                  type="text"
                  :value="formMode == 'add' ? '' : employee.IdentityNumber"
                />
                <span class="mes">{{ validateIdentityNumber }}</span>
              </div>
              <div class="m-col">
                <label>Ngày cấp</label>
                <input
                  id="txtIdentityDate"
                  type="date"
                  :value="formMode == 'add' ? '' : IdentityDate"
                />
              </div>
            </div>
            <div class="m-row" style="margin-bottom: 16px">
              <div class="m-col">
                <label>Nơi cấp</label>
                <input
                  id="txtIdentityPlace"
                  type="text"
                  :value="formMode == 'add' ? '' : employee.IdentityPlace"
                />
              </div>
            </div>

            <div class="m-row">
              <div class="m-col">
                <label>Email (<span>*</span>)</label>
                <input
                  id="txtEmail"
                  type="text"
                  :value="formMode == 'add' ? '' : employee.Email"
                />
                <span class="mes">{{ validateEmail }}</span>
              </div>
              <div class="m-col">
                <label>Số điện thoại (<span>*</span>)</label>
                <input
                  id="txtPhoneNumber"
                  type="text"
                  :value="formMode == 'add' ? '' : employee.PhoneNumber"
                />
                <span class="mes">{{ validatePhoneNumber }}</span>
              </div>
            </div>
            <div class="body-title">
              <div class="title-text">B. THÔNG TIN CÔNG VIỆC:</div>
              <div class="title-container"></div>
            </div>
            <div class="m-row" style="margin-bottom: 16px">
              <div class="m-col">
                <label>Vị trí</label>
                <select
                  id="cbPositionId"
                  :value="formMode == 'add' ? '' : employee.PositionId"
                >
                  <option value="3700cc49-55b5-69ea-4929-a2925c0f334d">
                    Giám đốc
                  </option>
                  <option value="148ed882-32b8-218e-9c20-39c2f00615e8">
                    Nhân viên Marketting
                  </option>
                  <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">
                    Thu ngân
                  </option>
                </select>
              </div>
              <div class="m-col">
                <label>Phòng ban</label>
                <select
                  id="cbDepartmentId"
                  :value="formMode == 'add' ? '' : employee.DepartmentId"
                >
                  <option value="17120d02-6ab5-3e43-18cb-66948daf6128">
                    Phòng đào tạo
                  </option>
                  <option value="4e272fc4-7875-78d6-7d32-6a1673ffca7c">
                    Phòng Công nghệ
                  </option>
                  <option value="469b3ece-744a-45d5-957d-e8c757976496">
                    Phòng nhân sự
                  </option>
                  <option value="142cb08f-7c31-21fa-8e90-67245e8b283e">
                    Phòng Marketting
                  </option>
                </select>
              </div>
            </div>
            <div class="m-row" style="margin-bottom: 16px">
              <div class="m-col">
                <label>Mã số thuế cá nhân</label>
                <input
                  id="txtPersonalTaxCode"
                  type="text"
                  :value="formMode == 'add' ? '' : employee.PersonalTaxCode"
                />
              </div>
              <div class="m-col">
                <label>Mức lương cơ bản</label>
                <!-- <input id="txtSalary" type="text" v-model="employee.Salary" /> -->
                <input
                  id="txtSalary"
                  type="number"
                  style="text-align: right"
                  :value="formMode == 'add' ? '' : employee.Salary"
                />
                <span class="unit"> (VNĐ)</span>
              </div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Ngày gia nhập công ty</label>
                <input
                  id="dtJoinDate"
                  type="date"
                  :value="formMode == 'add' ? '' : JoinDate"
                />
              </div>
              <div class="m-col">
                <label>Tình trạng công việc</label>
                <select
                  id="cbWorkStatus"
                  :value="formMode == 'add' ? '' : employee.WorkStatus"
                >
                  <option value="0">Đang thử việc</option>
                  <option value="1">Đang làm việc</option>
                  <option value="2">Đã nghỉ việc</option>
                </select>
              </div>
            </div>
          </div>
        </div>
        <div class="dialog-footer">
          <button id="btnSave" class="btn-default" @click="btnSaveOnClick()">
            <div class="icon-save"></div>
            Lưu
          </button>
          <button id="btnCancel" class="btn-default" @click="btnCloseOnClick()">
            Hủy
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import moment from "moment";
import $ from "jquery";

var newEmployee;

// function numberWithCommas(x) {
//   return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
// }

export default {
  props: {
    isHide: { type: Boolean, default: true },
    employeeId: { type: String, default: null },
    formMode: { type: String, default: null },
    newEmployeeCode: { type: String, default: null },
  },

  watch: {
    employeeId: function () {
      // Lấy dữ liệu từ Api:
      axios
        .get("http://api.manhnv.net/v1/employees/" + this.employeeId)
        .then((response) => {
          this.employee = response.data;
          this.dateOfBirth = moment(this.employee.dateOfBirth).format(
            "YYYY-MM-DD"
          );
          this.IdentityDate = moment(this.employee.IdentityDate).format(
            "YYYY-MM-DD"
          );
          this.JoinDate = moment(this.employee.JoinDate).format("YYYY-MM-DD");
        })
        .catch((res) => {
          alert(res.status);
        });
    },
  },
  updated() {
    // $('#txtEmployeeCode').
    if (this.isHide == false) {
      $("#txtEmployeeCode").focus();
      try {
        $("#txtEmployeeCode").val(newEmployee.EmployeeCode);
        $("#txtFullName").val(newEmployee.FullName);
        $("#dtDateOfBirth").val(newEmployee.DateOfBirth);
        $("#cbGender").val(newEmployee.Gender);
        $("#txtIdentityNumber").val(newEmployee.IdentityNumber);
        $("#txtIdentityDate").val(newEmployee.IdentityDate);
        $("#txtIdentityPlace").val(newEmployee.IdentityPlace);
        $("#txtEmail").val(newEmployee.Email);
        $("#txtPhoneNumber").val(newEmployee.PhoneNumber);
        $("#cbPositionId").val(newEmployee.PositionId);
        $("#cbDepartmentId").val(newEmployee.DepartmentId);
        $("#txtPersonalTaxCode").val(newEmployee.PersonalTaxCode);
        $("#dtJoinDate").val(newEmployee.JoinDate);
        $("#cbWorkStatus").val(newEmployee.WorkStatus);
        // $("#txtSalary").on("focus", function () {
        //   console.log("focuss");
        //   $("#txtSalary").attr("type", "text");
        //   $("#txtSalary").val(newEmployee.Salary);
        // });
        // $("#txtSalary").on("blur", function () {
        //   console.log("blurrr");
        //   $("#txtSalary").val(newEmployee.Salary);
        // });
        newEmployee = undefined;
      } catch (error) {
        return;
      }

      // this.$refs["text-some-input"].focus();
    }
  },
  methods: {
    btnCloseOnClick() {
      this.$emit("btnAddOnClick", true);
      this.validateEmployeeCode = null;
      this.validateFullName = null;
      this.validateIdentityNumber = null;
      this.validateEmail = null;
      this.validatePhoneNumber = null;
    },

    btnSaveOnClick() {
      var EmployeeCode = $("#txtEmployeeCode").val();
      var FullName = $("#txtFullName").val();
      var DateOfBirth = $("#dtDateOfBirth").val();
      var Gender = $("#cbGender").val();
      var IdentityNumber = $("#txtIdentityNumber").val();
      var IdentityDate = $("#txtIdentityDate").val();
      var IdentityPlace = $("#txtIdentityPlace").val();
      var Email = $("#txtEmail").val();
      var PhoneNumber = $("#txtPhoneNumber").val();
      var PositionId = $("#cbPositionId").val();
      var DepartmentId = $("#cbDepartmentId").val();
      var PersonalTaxCode = $("#txtPersonalTaxCode").val();
      var Salary = $("#txtSalary").val();
      var JoinDate = $("#dtJoinDate").val();
      var WorkStatus = $("#cbWorkStatus").val();

      newEmployee = {
        EmployeeCode: EmployeeCode,
        FullName: FullName,
        DateOfBirth: DateOfBirth,
        Gender: Gender,
        IdentityNumber: IdentityNumber,
        IdentityDate: IdentityDate,
        IdentityPlace: IdentityPlace,
        Email: Email,
        PhoneNumber: PhoneNumber,
        PositionId: PositionId,
        DepartmentId: DepartmentId,
        PersonalTaxCode: PersonalTaxCode,
        Salary: Salary,
        JoinDate: JoinDate,
        WorkStatus: WorkStatus,
      };

      if (!EmployeeCode) {
        this.validateEmployeeCode = "Yêu cầu nhập Mã nhân viên.";
      } else {
        this.validateEmployeeCode = null;
      }
      if (!FullName) {
        this.validateFullName = "Yêu cầu nhập Họ và tên.";
      } else {
        this.validateFullName = null;
      }
      if (!IdentityNumber) {
        this.validateIdentityNumber = "Yêu cầu nhập Số CMTND/ Căn cước.";
      } else {
        this.validateIdentityNumber = null;
      }
      var checkedEmail = true;
      if (!Email) {
        this.validateEmail = "Yêu cầu nhập địa chỉ Email.";
      } else {
        var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        if (!re.test(Email)) {
          this.validateEmail = "Email phải có định dạng example@abc.xyz";
          checkedEmail = false;
        } else {
          this.validateEmail = null;
        }
        // this.validateEmail = null;
      }
      if (!PhoneNumber) {
        this.validatePhoneNumber = "Yêu cầu nhập Số điện thoại.";
      } else {
        if (isNaN(PhoneNumber)) {
          this.validatePhoneNumber = "Số điện thoại chỉ gồm các chữ số.";
        } else {
          this.validatePhoneNumber = null;
        }
        // this.validatePhoneNumber = null;
      }

      if (
        EmployeeCode &&
        FullName &&
        IdentityNumber &&
        Email &&
        checkedEmail &&
        PhoneNumber &&
        !isNaN(PhoneNumber)
      ) {
        if (this.formMode == "add") {
          let seft = this;

          axios
            .post("http://api.manhnv.net/v1/employees/", newEmployee)
            .then(function (response) {
              console.log(response);
              seft.$emit("btnAddOnClick", true);
              seft.$emit("btnRefreshOnClick");
            })
            .catch(function (error) {
              console.log(error);

              seft.$emit("btnAddOnClick", true);
              seft.$emit("btnRefreshOnClick");
              alert(error);
            });
        } else if (this.formMode == "update") {
          let seft = this;
          axios
            .put(
              "http://api.manhnv.net/v1/employees/" + this.employeeId,
              newEmployee
            )
            .then(function (response) {
              console.log(response);
              seft.$emit("btnAddOnClick", true);
              seft.$emit("btnRefreshOnClick");
            })
            .catch(function (error) {
              console.log(error);
              seft.$emit("btnAddOnClick", true);
              seft.$emit("btnRefreshOnClick");
              alert(error);
            });
        }
      }
    },
  },

  data() {
    return {
      employee: {},
      dateOfBirth: "",
      IdentityDate: "",
      JoinDate: "",
      validate: {},
      validateFullName: null,
      validateEmployeeCode: null,
      validatePhoneNumber: null,
      validateEmail: null,
      validateIdentityNumber: null,
    };
  },
};
</script>
<style scoped>
#txtSalary {
  padding-right: 60px;
}
.unit {
  position: absolute;
  top: 31px;
  right: 20px;
  color: #000000 !important;
}
.m-col {
  width: 50%;
  float: left;
  padding: 0 4px;
  box-sizing: border-box;
  /* margin-bottom: 14px; */
}
.m-col span {
  color: red;
}
.m-col .mes {
  height: 16px;
  background-color: #fff;
  display: block;
}

.m-row {
  width: 100%;
  display: flex;
  /* margin-bottom: 14px; */
  position: relative;
}

.m-row label {
  display: block;
}

.m-row input,
select {
  margin-top: 4px;
}
.icon-add {
  transform: translateY(3px);
  display: inline-block;
  height: 20px;
  width: 20px;
  margin-right: 8px;
  background-size: contain;
  background-image: url("../../assets/icon/add.png");
}
.dialog .dialog-content {
  height: 730px;
  width: 740px;
  top: 44%;
  left: 42%;
}

.dialog .body-left {
  position: absolute;
  /* width: 200px; */
}
.dialog .body-right {
  position: absolute;
  left: 205px;
  width: 555px;
  /* height: 715px; */
}
.body-right .body-title {
  margin-left: 5px;
  margin-top: 20px;
}
.body-right .title-text {
  font-size: 15px;
}
.body-right .title-container {
  height: 4px;
  background-color: #019160;
  width: 85px;
  margin-top: 4px;
  margin-bottom: 10px;
}
.select-image {
  height: 160px;
  width: 160px;
  background-image: url("../../assets/img/default-avatar.jpg");
  background-size: contain;
  border-radius: 50%;
  border: 1px solid #bbbbbb;
  margin-top: 30px;
}
.body-left p {
  text-align: center;
  margin: 2px;
}
#btnSave {
  position: absolute;
  right: 20px;
  padding-left: 24px;
  padding-right: 24px;
}
.icon-save {
  display: inline-block;
  margin-right: 4px;
  transform: translateY(3px);
  height: 16px;
  width: 16px;
  background-image: url("../../assets/icon/add.png");
  background-size: contain;
}

#btnCancel {
  position: absolute;
  right: 150px;
  background-color: #e9ebee;
  color: #000000;
}
</style>
