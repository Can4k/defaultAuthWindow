<template>
<!--В этом же компоненте указать @closeWindow && :is-auth-window-active-->
  <transition name="fade" v-show="isAuthWindowActive">
    <div class="container-container">
      <div class="information-content" :class="'light'">
        <close-button @closeClicked="closeWindow"/>
        <h2>Авторизация</h2>
        <input
            class="inp"
            placeholder="Login"
            v-model = "this.currentLogin"
        >
        <div class="password-field">
          <input
              class="password inp"
              :type="isPasswordShow? 'text' : 'password'"
              placeholder="Password"
              v-model="this.currentPassword"
          >
          <change-pass-mode
              @changeShow="isPasswordShow = !isPasswordShow"
              :is-password-show="isPasswordShow"
          />
        </div>
        <footer>
          <div class="ok-button" @click="auth">
            <h3>ОК</h3>
          </div>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
import ChangePassMode from "@/components/authWindow/Buttons/changePassModeButton";
import CloseButton from "@/components/authWindow/Buttons/closeButton";
export default {
  name: "auntification.vue",
  components: {CloseButton, ChangePassMode},
  methods: {
    async auth() {
      let ans = await fetch('http://localhost:7777')
          .then((response) => {
            return response.json();
          });
      if (ans.isAdmin === true) {
        console.log("Ура, вы админ!!!!");
        this.closeWindow();
      }
    },
    closeWindow() {
      this.$emit("closeWindow");
    }
  },
  props: {
    isAuthWindowActive: Boolean
  },
  data() {
    return {
      isPasswordShow: false,
      currentPassword: "",
      currentLogin: ""
    }
  }
}
</script>

<style scoped>
* {
  transition-duration: .1s;
  user-select: none;
  font-family: 'Nunito', sans-serif;
}

.container-container {
  z-index: 10;
}

.information-content {
  width: 400px;
  margin-top: 50px;
  position: absolute;
  left: 50%;
  transform: translate(-50%);
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0 4px 50px -12px rgba(17, 12, 46, 0.16);
  display: flex;
  flex-direction: column;
  border: 1px solid rgba(196, 187, 187, 0.24);
}

.show-pass {
  cursor: pointer;
  width: 18px;
  height: 18px;
  border-radius: 3px;
  position: absolute;
  top: 154px;
  right: 21px;
}

.inp {
  box-shadow: 0 4px 10px -5px rgba(17, 12, 46, 0.07);
  border-radius: 5px;
  height: 30px;
  border: 1px solid rgba(196, 187, 187, 0.24);
  margin: 4px;
  font-size: 13px;
  font-weight: 1000;
  transition-duration: .3s;
  padding: 2px 2px 2px 7px;
}

.password {
  width: 370px;
}

.inp:focus {
  transform: translate(3px);
}

.information-content h2 {
  font-size: 35px;
  text-align: center;
  margin-bottom: 20px;
}

.information-content b {
  font-size: 13px;
}

.information-content footer {
  display: flex;
  justify-content: center;
}

.light {
  color: black;
  background-color: white;
}

footer h3 {
  background-color: #42b983;
  box-shadow: 0 4px 50px -12px rgba(17, 12, 46, 0.16);
  border: 1px solid rgba(196, 187, 187, 0.24);
  color: white;
  padding: 2px 20px 2px 20px;
  border-radius: 5px;
  margin-top: 10px;
  user-select: none;
  font-size: 15px;
  transition-duration: .2s;
}

footer h3:hover {
  background-color: rgba(66, 185, 131, 0.76);
  cursor: pointer;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity .2s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media screen and (max-width: 740px) {
  .information-content {
    border-radius: 10px;
    padding: 10px;
    font-family: 'Nunito', sans-serif;
    z-index: 2;
    width: 310px;
  }
  .password {
    width: 280px;
  }
}
</style>