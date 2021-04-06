<template>
  <div>
    <div class="page-title">
      <div class="page-left">Danh sách nhân viên</div>
      <div class="page-right">
        <button id="btnAdd" class="btn-default" @click="btnAddOnClick()">
          <div class="icon-add"></div>
          Thêm Nhân viên
        </button>
      </div>
    </div>
    <div class="toolbar">
      <input
        type="text"
        class="input-search"
        style="width: 360px"
        placeholder="Tìm kiếm theo Mã, Tên hoặc Số điện thoại"
      />
      <div class="custom-select" style="width: 230px; margin-left: 20px">
        <select name="" id="">
          <option value="0">Tất cả phòng ban</option>
          <option value="3700cc49-55b5-69ea-4929-a2925c0f334d">Giám đốc</option>
          <option value="148ed882-32b8-218e-9c20-39c2f00615e8">
            Nhân viên Marketting
          </option>
          <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Thu ngân</option>
        </select>
      </div>
      <div class="custom-select" style="width: 180px; margin-left: 20px">
        <select name="" id="">
          <option value="0">Tất cả vị trí</option>
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

      <button
        id="btnRefresh"
        class="btn-refresh"
        @click="btnRefreshOnClick()"
      ></button>
      <button
        id="btnDelete"
        class="btn-delete"
        @click="btnDeleteOnClick()"
      ></button>
    </div>
    <div class="grid">
      <table id="tblListEmployee" class="table" width="100%" border="0">
        <thead>
          <tr>
            <th>Mã nhân viên</th>
            <th>Họ và tên</th>
            <th>Giới tính</th>
            <th>Ngày sinh</th>
            <th>Điện thoại</th>
            <th>Email</th>
            <th>Vị trí/ Chức vụ</th>
            <th>Phòng ban</th>
            <th class="text-align-right">Múc lương cơ bản</th>
            <th class="text-align-center">Tình trạng công việc</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="employee in employees"
            :key="employee.EmployeeId"
            @dblclick="rowOnDblClick(employee.EmployeeId, employee)"
            class="trEmployee"
          >
            <td>{{ employee.EmployeeCode }}</td>
            <td>{{ employee.FullName }}</td>
            <td>{{ employee.GenderName }}</td>
            <td>{{ moment(employee.DateOfBirth).format("DD/MM/YYYY") }}</td>
            <td>{{ employee.PhoneNumber }}</td>
            <td>{{ employee.Email }}</td>
            <td>{{ employee.PositionName }}</td>
            <td>{{ employee.DepartmentName }}</td>
            <td class="text-align-right">{{ employee.Salary }}</td>
            <td class="text-align-center">{{ employee.WorkStatusName }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="paging">
      <div class="paging-left">Hiển thị 1-10/1000 khách hàng</div>
      <div class="paging-center">
        <div class="btn-firstpage">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-chevrons-left"
          >
            <polyline points="11 17 6 12 11 7"></polyline>
            <polyline points="18 17 13 12 18 7"></polyline>
          </svg>
        </div>
        <div class="btn-prev-page">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-chevron-left"
          >
            <polyline points="15 18 9 12 15 6"></polyline>
          </svg>
        </div>
        <div class="btn-page">
          <div class="btn-page-index active">1</div>
          <div class="btn-page-index">2</div>
          <div class="btn-page-index">3</div>
          <div class="btn-page-index">4</div>
        </div>
        <div class="btn-next-page">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-chevron-right"
          >
            <polyline points="9 18 15 12 9 6"></polyline>
          </svg>
        </div>
        <div class="btn-lastpage">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-chevrons-right"
          >
            <polyline points="13 17 18 12 13 7"></polyline>
            <polyline points="6 17 11 12 6 7"></polyline>
          </svg>
        </div>
      </div>
      <div class="paging-right">10 khách hàng/trang</div>
    </div>
    <div id="myModal" class="modal">
      <!-- Modal content -->
      <div class="modal-content">
        <div class="modal-header">
          <span class="close">&times;</span>
          <div class="title">Xóa</div>
        </div>
        <div class="modal-body">
          <div class="warning-icon icon-left"></div>
          <div class="content">
            Bạn có chắc chắn muốn xóa {{ employee.EmployeeCode }} không ?
          </div>
        </div>
        <div class="modal-footer">
          <div id="btnCancelEmployee" class="btn-default">Hủy</div>
          <div id="btnDeleteEmployee" class="btn-default">Xóa</div>
        </div>
      </div>
    </div>

    <EmployeeDetail
      :isHide="isHideDialogDetail"
      :employeeId="employeeId"
      :formMode="detailFormMode"
      @btnAddOnClick="btnAddOnClick"
      @btnRefreshOnClick="btnRefreshOnClick"
    />
  </div>
</template>
<script>
import axios from "axios";
import EmployeeDetail from "./EmployeeDetail.vue";
// import Modal from "../../components/modals/Modal.vue";
import moment from "moment";
import $ from "jquery";

export default {
  components: {
    EmployeeDetail,
    // Modal,
  },
  created() {
    axios.get("http://api.manhnv.net/v1/employees").then((response) => {
      console.log(response);
      this.employees = response.data;
    });
  },

  methods: {
    btnDeleteOnClick() {
      this.deleteTrue = !this.deleteTrue;
      if (this.deleteTrue == true) {
        console.log("DeleteOnClick");
        $(".trEmployee").css("background-color", "#FFEBEB");
        $(".trEmployee").hover(
          function () {
            $(this).css("background-color", "#F65454");
          },
          function () {
            $(this).css("background-color", "#FFEBEB");
          }
        );
      } else {
        $(".trEmployee").unbind("mouseenter mouseleave");
        $(".trEmployee").css("background-color", "");
      }
    },
    btnRefreshOnClick() {
      axios.get("http://api.manhnv.net/v1/employees").then((response) => {
        console.log(response);
        this.employees = response.data;
      });
    },
    btnAddOnClick(isShowDialog) {
      this.detailFormMode = "add";

      if (isShowDialog == true) {
        this.isHideDialogDetail = true;
      } else {
        this.isHideDialogDetail = false;
      }
    },
    rowOnDblClick(employeeId, employee) {
      if (this.deleteTrue == true) {
        let seft1 = this;
        this.employee = employee;
        $(".modal").css("display", "block");
        $("#btnDeleteEmployee").on("click", function () {
          let seft2 = seft1;
          axios
            .delete("http://api.manhnv.net/v1/employees/" + employeeId)
            .then(function (response) {
              seft2.btnRefreshOnClick();
              seft2.deleteTrue = false;
              $(".trEmployee").unbind("mouseenter mouseleave");
              $(".trEmployee").css("background-color", "");
              $(".modal").css("display", "none");
              console.log(response);
            })
            .catch(function (error) {
              console.log(error);
              $(".modal").css("display", "none");
            });
        });
      } else {
        this.employeeId = employeeId;
        this.isHideDialogDetail = false;
        this.detailFormMode = "update";
      }
    },
  },
  data() {
    return {
      isHideDialogDetail: true,
      employeeId: null,
      detailFormMode: null,
      employee: {},
      employees: [],
      moment: moment,
      deleteTrue: false,
    };
  },
  mounted() {
    // Modal js
    var modal = document.getElementById("myModal");
    var span = document.getElementsByClassName("close")[0];
    var cancle = document.getElementById("btnCancelEmployee");
    span.onclick = function () {
      modal.style.display = "none";
    };
    cancle.onclick = function () {
      modal.style.display = "none";
    };
    window.onclick = function (event) {
      if (event.target == modal) {
        modal.style.display = "none";
      }
    };

    // Select js
    var x, i, j, l, ll, selElmnt, a, b, c;
    x = document.getElementsByClassName("custom-select");
    l = x.length;
    for (i = 0; i < l; i++) {
      selElmnt = x[i].getElementsByTagName("select")[0];
      ll = selElmnt.length;
      a = document.createElement("DIV");
      a.setAttribute("class", "select-selected");
      a.innerHTML = selElmnt.options[selElmnt.selectedIndex].innerHTML;
      x[i].appendChild(a);
      b = document.createElement("DIV");
      b.setAttribute("class", "select-items select-hide");
      for (j = 1; j < ll; j++) {
        c = document.createElement("DIV");
        c.innerHTML = selElmnt.options[j].innerHTML;
        c.addEventListener("click", function () {
          var y, i, k, s, h, sl, yl;
          s = this.parentNode.parentNode.getElementsByTagName("select")[0];
          sl = s.length;
          h = this.parentNode.previousSibling;
          for (i = 0; i < sl; i++) {
            if (s.options[i].innerHTML == this.innerHTML) {
              s.selectedIndex = i;
              h.innerHTML = this.innerHTML;
              y = this.parentNode.getElementsByClassName("same-as-selected");
              yl = y.length;
              for (k = 0; k < yl; k++) {
                y[k].removeAttribute("class");
              }
              this.setAttribute("class", "same-as-selected");
              break;
            }
          }
          h.click();
        });
        b.appendChild(c);
      }
      x[i].appendChild(b);
      a.addEventListener("click", function (e) {
        e.stopPropagation();
        closeAllSelect(this);
        this.nextSibling.classList.toggle("select-hide");
        this.classList.toggle("select-arrow-active");
      });
    }
    function closeAllSelect(elmnt) {
      var x,
        y,
        i,
        xl,
        yl,
        arrNo = [];
      x = document.getElementsByClassName("select-items");
      y = document.getElementsByClassName("select-selected");
      xl = x.length;
      yl = y.length;
      for (i = 0; i < yl; i++) {
        if (elmnt == y[i]) {
          arrNo.push(i);
        } else {
          y[i].classList.remove("select-arrow-active");
        }
      }
      for (i = 0; i < xl; i++) {
        if (arrNo.indexOf(i)) {
          x[i].classList.add("select-hide");
        }
      }
    }
    document.addEventListener("click", closeAllSelect);
  },
};
</script>
<style scope>
.warning-icon {
  height: 40px;
  width: 40px;
  background-size: contain;
  border-radius: 50%;
  background-repeat: no-repeat;
  background-color: #e9ebee;
  background-image: url("../../assets/img/warning.png");
}
#btnCancelEmployee {
  position: absolute;
  right: 150px;
  top: 10px;
  background-color: #e9ebee;
  color: #000;
  padding-left: 40px;
  padding-right: 40px;
}
#btnDeleteEmployee {
  position: absolute;
  right: 24px;
  top: 10px;
  background-color: #f65454;
  color: #fff;
  padding-left: 40px;
  padding-right: 40px;
}
.page-title {
  height: 40px;
  display: flex;
  align-items: center;
}

.page-title .page-right {
  position: absolute;
  right: 24px;
}

.page-title .page-left {
  font-size: 24px;
  font-weight: bold;
}
/* 
.paging-bar {
  border-top: 4px solid #bbbbbb;
} */

.toolbar {
  margin-top: 16px;
  display: flex;
  width: 100%;
  align-items: center;
  height: 42px;
  /* background-color: #ff0000; */
}

.grid {
  position: absolute;
  right: 24px;
  left: 24px;
  bottom: 60px;
  top: 128px;
  overflow-y: auto;
}

.paging {
  position: absolute;
  bottom: 0;
  height: 60px;
  left: 24px;
  right: 24px;
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

/* The container must be positioned relative: */
.custom-select {
  position: relative;
  font-family: Arial;
}

.custom-select select {
  display: none; /*hide original SELECT element: */
}

.select-selected {
  font-size: 13px;
  background-color: #fff;
  height: 40px;
  border: 1px solid #bbbbbb;
  padding-left: 12px;
  padding-right: 12px;
  border-radius: 4px;
  box-sizing: border-box;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
.select-selected:hover {
  border: 1px solid #019160;
}
.select-selected:active {
  border: 1px solid #019160;
}

/* Style the arrow inside the select element: */
.select-selected:after {
  position: absolute;
  content: "";
  top: 16px;
  right: 12px;
  width: 0;
  height: 0;
  border: 6px solid #bbbbbb;
  border-color: #000 transparent transparent transparent;
}

/* Point the arrow upwards when the select box is open (active): */
.select-selected.select-arrow-active:after {
  border-color: transparent transparent #000 transparent;
  top: 7px;
}

/* style the items (options), including the selected item: */
.select-items div,
.select-selected {
  color: #000;
  padding: 8px 16px;
  cursor: pointer;
}
.select-items div {
  height: 24px;
}
.select-items div:hover {
  background-color: #e9ebee;
}
.select-items div:active {
  background-color: #019160;
  color: #fff;
}
/* Style items (options): */
.select-items {
  position: absolute;
  background-color: #fff;
  top: 100%;
  left: 0;
  right: 0;
  z-index: 99;
  box-shadow: 0px 2px 5px 1px #bbbbbb;
}

/* Hide the items when the select box is closed: */
.select-hide {
  display: none;
}
</style>