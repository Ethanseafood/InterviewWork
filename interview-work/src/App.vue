<template>
  <div>
    <nav class="navbar-light bg-light">
      <div class="container d-flex justify-content-evenly">
        <div class="login">
          <img
            src="@/assets/memberIcon.png"
            class="cursor-pointer icon"
            alt="member icon"
            width="30"
            height="30"
            @click="toggleLoginPopup"
          />
          <span id="memberName" class="navbar-text">{{ memberName }}</span>
        </div>
        <div>
          <img
            src="@/assets/imageIcon.png"
            class="cursor-pointer icon"
            alt="image icon"
            width="30"
            height="30"
            @click="toggleImagePopup"
          />
        </div>
        <div class="calendar">
          <input
            type="date"
            id="start"
            name="trip-start"
            min="2018-01-01"
            max="2023-12-31"
          />
        </div>
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
                  autocomplete="off"
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
                  autocomplete="off"
                />
              </div>
            </div>
            <div class="field">
              <label for="passConf" class="label">再次確認密碼</label>
              <div class="control">
                <input
                  id="passConf"
                  v-model="confirmPassword"
                  class="input"
                  type="password"
                  placeholder="請輸入密碼"
                  @keyup="validateConfirmPassword"
                />
                <span
                  id="passwordLengthLimit"
                  v-if="password.length < 8 && password.length != 0"
                  >字數需要大於8位</span
                >
                <br />
                <span id="passwordNotMatch" v-if="password !== confirmPassword"
                  >密碼不一致</span
                >
              </div>
            </div>
            <div class="field">
              <div class="control">
                <button
                  :disabled="
                    password.length < 8 ||
                    password !== confirmPassword ||
                    username.length == 0
                  "
                  type="submit"
                  class="button is-primary"
                >
                  提交
                </button>
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
      confirmPassword: "",
      memberName: "", 
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
.container {
  display: flex;
}
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

#passwordLengthLimit,
#passwordNotMatch {
  color: red;
}
</style>
