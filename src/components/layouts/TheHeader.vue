<template>
  <div>
    <div id="header">
      <div class="left">
        <div class="left-text">Nhà hàng Biển Đông</div>
        <div class="left-icon">
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
            <polyline points="0 13 7 20 13 13"></polyline>
          </svg>
        </div>
      </div>
      <div class="right">
        <div class="right-avatar"></div>
        <div class="right-name">Nguyễn Văn Mạnh</div>
        <div class="right-option"></div>
      </div>
    </div>
  </div>
</template>
<style scoped>
#header {
  border: 1px solid #dedede;
  position: absolute;
  left: 200px;
  right: 0;
  height: 60px;
  top: 0;
}
.left {
  position: absolute;
  margin-left: 16px;
  margin-top: 12px;
}
.left .left-text {
  font-size: 15px;
  font-weight: bold;
  display: inline-flex;
}
.left .left-icon {
  margin-left: 10px;
  display: inline-flex;
  cursor: pointer;
  transform: translateY(3px);
}
.right {
  position: absolute;
  right: 0;
}
.right .right-avatar {
  height: 40px;
  width: 40px;
  background-image: url("../../assets/icon/avatar-default.png");
  background-size: contain;
  margin-right: 16px;
  display: inline-flex;
  transform: translateY(10px);
  cursor: pointer;
}
.right .right-name {
  display: inline-flex;
  font-size: 15px;
  margin-right: 16px;
  padding-bottom: 10px;
  cursor: pointer;
  transform: translateY(-3px);
}
.right .right-option {
  transform: translateY(4px);
  margin-right: 16px;
  cursor: pointer;
  height: 24px;
  width: 24px;
  background-size: contain;
  display: inline-flex;
  background-image: url("../../assets/icon/option.png");
}
</style>