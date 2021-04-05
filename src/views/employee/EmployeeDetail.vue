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
                  id="txtEmployeeCode"
                  type="text"
                  v-model="employee.EmployeeCode"
                />
              </div>
              <div class="m-col">
                <label>Họ và tên (<span>*</span>)</label>
                <input
                  id="txtFullName"
                  type="text"
                  v-model="employee.FullName"
                />
              </div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Ngày sinh</label>
                <input id="dtDateOfBirth" type="date" v-model="dateOfBirth" />
              </div>
              <div class="m-col">
                <label>Giới tính</label>
                <select id="cbGender" v-model="employee.Gender">
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
                  v-model="employee.IdentityNumber"
                />
              </div>
              <div class="m-col">
                <label>Ngày cấp</label>
                <input
                  id="txtIdentityDate"
                  type="date"
                  v-model="IdentityDate"
                />
              </div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Nơi cấp</label>
                <input
                  id="txtIdentityPlace"
                  type="text"
                  v-model="employee.IdentityPlace"
                />
              </div>
            </div>

            <div class="m-row">
              <div class="m-col">
                <label>Email (<span>*</span>)</label>
                <input id="txtEmail" type="text" v-model="employee.Email" />
              </div>
              <div class="m-col">
                <label>Số điện thoại (<span>*</span>)</label>
                <input
                  id="txtPhoneNumber"
                  type="text"
                  v-model="employee.PhoneNumber"
                />
              </div>
            </div>
            <div class="body-title">
              <div class="title-text">B. THÔNG TIN CÔNG VIỆC:</div>
              <div class="title-container"></div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Vị trí</label>
                <select id="cbPositionId" v-model="employee.PositionId">
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
                <select id="cbDepartmentId" v-model="employee.DepartmentId">
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
            <div class="m-row">
              <div class="m-col">
                <label>Mã số thuế cá nhân</label>
                <input
                  id="txtPersonalTaxCode"
                  type="text"
                  v-model="employee.PersonalTaxCode"
                />
              </div>
              <div class="m-col">
                <label>Mức lương cơ bản</label>
                <input id="txtSalary" type="text" v-model="employee.Salary" />
              </div>
            </div>
            <div class="m-row">
              <div class="m-col">
                <label>Ngày gia nhập công ty</label>
                <input id="dtJoinDate" type="date" v-model="JoinDate" />
              </div>
              <div class="m-col">
                <label>Tình trạng công việc</label>
                <select id="cbWorkStatus" v-model="employee.WorkStatus">
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
          <button id="btnCancel" class="btn-default">Hủy</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import moment from "moment";
export default {
  props: {
    isHide: { type: Boolean, default: true },
    employeeId: { type: String, default: null },
    formMode: { type: Number, default: null },
  },
  created() {},
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
          console.log(response.data);
        })
        .catch((res) => {
          alert(res.status);
        });
    },
  },
  methods: {
    btnCloseOnClick() {
      this.$emit("btnAddOnClick", true);
    },
    /**
     * Thực hiện cất dữ liệu
     * CreatedBy: NVMANH (29/03/2021)
     * ModifiedBy: NVThang - sửa lại cơ chế cất dữ liệu (30/03/2021)
     * ModifiedBy: NVThang - sửa lại cơ chế cất dữ liệu (30/03/2021)
     */
    btnSaveOnClick() {
      // Lấy id của khách hàng:
      // var employeeID = this.employeeID;
      // Kiểm tra trạng thái của form (là thêm mới hay là sửa):
      // Gọi service thực hiện cất dữ liệu:
      if (this.formMode == "add") {
        axios.post("", this.employee);
      } else {
        axios.post("", this.employee);
      }

      // Kiểm tra kết quả của việc cất dữ liệu"
    },
  },
  data() {
    return {
      employee: {},
      dateOfBirth: "",
      IdentityDate: "",
      JoinDate: "",
    };
  },
};
</script>
<style scoped>
.m-col {
  width: 50%;
  float: left;
  padding: 0 4px;
  box-sizing: border-box;
}
.m-col span {
  color: red;
}

.m-row {
  width: 100%;
  display: flex;
  margin-top: 8px;
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
  height: 685px;
  width: 740px;
  top: 46%;
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
}
.body-right .body-title {
  margin-left: 5px;
  margin-top: 25px;
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
