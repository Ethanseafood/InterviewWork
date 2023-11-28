<template>
  <div>
    <nav class="navbar navbar-light bg-light">
      <div class="container">
        <img
          src="@/assets/memberIcon.png"
          class="cursor-pointer icon"
          alt="member icon"
          width="30"
          height="30"
          @click="toggleLoginPopup"
        />
        <span id="memberName" class="navbar-text">{{ memberName }}</span>
        <img
          src="@/assets/imageIcon.png"
          class="cursor-pointer icon"
          alt="image icon"
          width="30"
          height="30"
          @click="toggleImagePopup"
        />
        <img
          src="@/assets/calendarIcon.png"
          class="cursor-pointer icon"
          alt="calendar icon"
          width="30"
          height="30"
        />
      </div>
    </nav>

    <!-- 彈出視窗 -->
    <div class="modal" :class="{ 'is-active': showLoginPopup }">
      <div class="modal-background" @click="closeLoginPopup"></div>
      <div class="modal-content">
        <div class="box">
          <h3 class="title">登入</h3>
          <form @submit.prevent="submitForm">
            <!-- 表單內容 -->
            <div class="field">
              <label class="label">使用者名稱</label>
              <div class="control">
                <input
                  v-model="username"
                  class="input"
                  type="text"
                  placeholder="請輸入使用者名稱"
                />
              </div>
            </div>
            <div class="field">
              <label class="label">密碼</label>
              <div class="control">
                <input
                  v-model="password"
                  class="input"
                  type="password"
                  placeholder="請輸入密碼"
                />
              </div>
            </div>
            <div class="field">
              <div class="control">
                <button type="submit" class="button is-primary">提交</button>
              </div>
            </div>
          </form>
        </div>
      </div>
      <button
        class="modal-close is-large"
        aria-label="close"
        @click="closeLoginPopup"
      ></button>
    </div>
  </div>
  <div class="modal" :class="{ 'is-active': showImagePopup }">
    <div class="modal-background" @click="closeImagePopup"></div>
    <div class="modal-content">
      <img src="@/assets/image.jpg" alt="image" />
      <button
        class="modal-close is-large"
        aria-label="close"
        @click="closeImagePopup"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showLoginPopup: false,
      showImagePopup: false,
      username: "",
      password: "",
      memberName: "", // 顯示使用者名稱
    };
  },
  methods: {
    toggleLoginPopup() {
      this.showLoginPopup = !this.showLoginPopup;
    },
    closeLoginPopup() {
      this.showLoginPopup = false;
    },
    submitForm() {
      // 在這裡處理表單提交，例如驗證使用者名稱和密碼
      // 假設表單驗證成功，將使用者名稱設置並關閉彈出視窗
      this.memberName = this.username;
      this.closeLoginPopup();
    },
    toggleImagePopup() {
      this.showImagePopup = !this.showImagePopup;
    },
    closeImagePopup() {
      this.showImagePopup = false;
    },
  },
};
</script>

<style>
@import "bulma/css/bulma.css";
.modal {
  display: none;
}

.modal.is-active {
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background-color: white; /* 设定 Modal 内容的背景颜色 */
  max-width: 400px;
  margin: auto; /* 水平居中 */
}

.modal-background {
  background-color: rgba(0, 0, 0, 0.5); /* 使用 rgba 设置半透明黑色 */
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

.modal-background,
.modal-content,
.modal-close {
  z-index: 10; /* 確保模態框在最上層 */
}
.cursor-pointer {
  cursor: pointer;
}
</style>
