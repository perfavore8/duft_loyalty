<template>
  <div class="app">
    <div class="logo"></div>
    <div class="container" v-if="!showModal">
      <div class="head_radio_btn_group">
        <div class="head_radio_btn_item">
          <input
            type="radio"
            name="head_selector"
            id="head_selector1"
            checked
          />
          <label for="head_selector1"
            ><div id="head_selector_icon1" />
            ПОКУПАТЕЛЬ</label
          >
        </div>
        <div class="head_radio_btn_item">
          <input type="radio" name="head_selector" id="head_selector2" />
          <label for="head_selector2"
            ><div id="head_selector_icon2" />
            PRO</label
          >
        </div>
      </div>
      <div class="content">
        <div id="auth">авторизация</div>
        <div class="phone">
          <label for="phone">Телефон:</label>
          <div
            class="phone_with_selector"
            :class="{
              notvalid: Validation.phone === false,
            }"
          >
            <select>
              <option></option>
            </select>
            <input
              type="text"
              v-model="phone"
              placeholder="+7 (___) ___ - __ - __"
              @input="onlyNumbers()"
              maxlength="12"
              minlength="12"
            />
          </div>
        </div>
        <template v-if="Validation.phone === false"
          ><div class="error">
            <div id="error_logo" />
            <label class="error_number">Неверный номер телефона</label>
          </div></template
        >
        <div
          class="accepte"
          :class="{
            shortM: Validation.phone === false,
          }"
        >
          <input
            type="checkbox"
            id="check"
            v-model="Validation.check"
            :class="{
              error_ac: Validation.check === false,
            }"
          />
          <label for="check" class="check_label"></label>
          <label class="text_check_label"
            >Я соглашаюсь на передачу и обработку персональных данных и
            подтверждаю свое совершеннолетие.</label
          >
        </div>
        <template v-if="Validation.check === false"
          ><div class="error">
            <div id="error_logo" />
            <label class="error_number">Необходимо дать согласие</label>
          </div></template
        >
        <div class="select">
          <label>Авторизоваться через:</label>
          <div class="form_radio_btn_group">
            <div class="form_radio_btn_item">
              <input type="radio" name="messenger" id="messenger1" checked />
              <label for="messenger1"
                ><div id="icon_messenger1" />
                SMS</label
              >
            </div>
            <div class="form_radio_btn_item">
              <input type="radio" name="messenger" id="messenger2" />
              <label for="messenger2"
                ><div id="icon_messenger2" />
                WhatsApp</label
              >
            </div>
            <div class="form_radio_btn_item">
              <input type="radio" name="messenger" id="messenger3" />
              <label for="messenger3"
                ><div id="icon_messenger3" />
                Telegram</label
              >
            </div>
          </div>
        </div>
        <button id="code" @click="secondReg()">Получить код</button>
      </div>
    </div>
  </div>
  <div class="modal" v-if="showModal">
    <div class="modal_container">
      <div class="modal_icon" />
      <label class="modal_name">Ошибка</label
      ><label class="modal_body"
        >Необходимо согласие с передачей и обработкой персональных
        данных.</label
      ><button class="modal_btn" @click="closeModal()">ОК</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      Validation: {
        phone: null,
        check: null,
      },
      phone: "",
      showModal: false,
    };
  },
  methods: {
    onlyNumbers() {
      const prefix = this.phone.slice(0, 2);
      const endNumber = this.phone.slice(2, 12);
      this.Validation.phone =
        !/^[\d]{11}$/.test(endNumber) &&
        prefix === "+7" &&
        endNumber.length == 10
          ? true
          : null;
    },

    secondReg() {
      const phone = this.Validation.phone;
      const check = this.Validation.check;
      const windowInnerWidth = window.innerWidth;
      if (
        phone &&
        phone != null &&
        check &&
        check != null &&
        windowInnerWidth > 600
      ) {
        alert("ok");
      } else {
        if (phone === null) {
          this.Validation.phone = false;
        }
        if (check === null) {
          this.Validation.check = false;
        }
        if (windowInnerWidth <= 600) {
          this.showModal = true;
        }
      }
    },
    closeModal() {
      this.showModal = false;
      this.Validation.phone = null;
      this.Validation.check = null;
    },
  },
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700;900&display=swap");
@mixin _600 {
  @media (max-width: 600px) {
    @content;
  }
}

@mixin bg_image($url, $size: 100% 100%) {
  background-size: $size;
  background-repeat: no-repeat;
  background-position: center center;
  background-image: url($url);
}

@mixin font($w, $s, $h) {
  font-family: "Roboto";
  font-style: normal;
  font-weight: $w;
  font-size: $s;
  line-height: $h;
}

.notvalid {
  border: 1px solid #d13c3c !important;
  box-shadow: 0px 0px 4px 4px rgba(209, 60, 60, 0.25);
}

.app {
  display: flex;
  flex-direction: column;

  width: 100vw;
  height: 100vh;

  background-size: 100% 100%;
  background-repeat: no-repeat;
  background-position: center center;
  background: url("../assets/image 13.jpg") no-repeat 100% 100%;

  user-select: none;
}

.logo {
  width: 95.8px;
  height: 80px;
  margin: 60px auto;

  @include bg_image("../assets/logo.svg");

  @include _600 {
    width: 70px;
    height: 60px;
    margin: 30px auto 38px;
  }
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;

  width: 557px;
  // max-height: 600px;
  margin: 0 auto;

  background: #172144;

  @include _600 {
    width: 280px;
  }
}
.head_radio_btn_group {
  display: inline-block;
  overflow: hidden;
  > .head_radio_btn_item {
    display: inline-block;
    float: left;
    > label {
      width: 277px;
      height: 60px;

      display: flex;
      align-items: center;
      justify-content: center;

      @include font(700, 15px, 20px);
      text-transform: uppercase;

      color: #9994b5;
      background: #101727;

      cursor: pointer;
      user-select: none;

      @include _600 {
        width: 140px;
        height: 40px;
        @include font(700, 12px, 20px);
      }
      > #head_selector_icon1 {
        mask-image: url("../assets/Buyer.svg");
      }
      > #head_selector_icon2 {
        mask-image: url("../assets/PRO.svg");
      }
      > div {
        width: 20px;
        height: 20px;
        margin-right: 8px;
        mask-size: 80% 80%;
        mask-repeat: no-repeat;
        mask-position: center center;
        background-color: #8b90a1;
      }
    }
    > input {
      display: none;
    }
  }
  > .head_radio_btn_item input:checked + label {
    color: #ffffff;
    background: #172144;
    border-top: 2px solid #ff00b1;
    > div {
      background-color: #ff00b1;
    }
  }
}
.content {
  width: 360px;
  @include _600 {
    width: 240px;
  }
  > #auth {
    width: 360px;
    height: 25px;

    margin: 60px auto 0px;

    @include font(900, 30px, 20px);

    text-align: center;
    text-transform: uppercase;

    color: #ffffff;

    @include _600 {
      width: 240px;
      height: 25px;

      margin: 40px auto 0px;

      @include font(900, 20px, 20px);
    }
  }
  > .phone {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin: 35px auto 0px;

    @include _600 {
      margin: 20px auto 0px;
    }
    > label {
      width: 65px;
      height: 16px;

      @include font(400, 15px, 16px);

      color: #9994b5;
    }
    > .phone_with_selector {
      display: flex;
      flex-direction: raw;

      width: 360px;
      height: 48px;

      background: rgba(16, 23, 39, 0.5);
      border: 1px solid rgba(153, 148, 181, 0.1);
      border-radius: 8px;

      @include _600 {
        width: 240px;
      }
      > select {
        width: 48px;
        height: 48px;
        border-radius: 8px 0 0 8px;

        background: rgba(16, 23, 39, 0.5);
        border: none;
        outline: none;

        @include bg_image("../assets/countryes/Russia.svg", 22px 22px);
        background-position: 9px center;

        color: #ffffff80;

        cursor: pointer;

        @include _600 {
        }
      }
      > input[type="number"]::-webkit-outer-spin-button,
      input[type="number"]::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
      }
      > input {
        box-sizing: border-box;
        box-shadow: none;

        width: 310px;
        height: 48px;

        background: rgba(16, 23, 39, 0.5);
        border: none;

        padding-left: 8px;

        @include font(400, 20px, 20px);

        color: #9994b5;
        outline: none;

        @include _600 {
          width: 190px;
        }
      }
    }
  }
  > .accepte {
    display: flex;
    flex-direction: row;
    gap: 12px;
    margin: 20px auto 0px;
    > .check_label {
      box-sizing: border-box;

      width: 16px;
      height: 16px;

      background: rgba(16, 23, 39, 0.5);
      border: 1px solid rgba(255, 255, 255, 0.5);
      border-radius: 2px;

      cursor: pointer;
      user-select: none;

      @include _600 {
      }
    }
    > input:checked + label {
      background: #ff00b1;
      @include bg_image("../assets/path4483.svg", 70% 70%);
    }
    > input {
      display: none;
    }
    > .text_check_label {
      width: 333px;
      height: 41px;

      @include font(400, 12px, 20px);

      color: #9994b5;

      @include _600 {
        width: 195px;
      }
    }
  }
  > .select {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin: 47px auto 0px;

    @include _600 {
      margin: 57px auto 0px;
    }
    > label {
      width: 163px;
      height: 16px;

      @include font(400, 15px, 16px);

      color: #9994b5;
    }
    > .form_radio_btn_group {
      display: inline-block;
      overflow: hidden;
      background: #141c35;
      border-radius: 100px;

      > .form_radio_btn_item {
        display: inline-block;
        float: left;
        > label {
          width: 120px;
          height: 48px;

          display: flex;
          align-items: center;
          justify-content: center;

          @include font(400, 15px, 16px);

          color: #9994b5;
          background: #141c35;

          cursor: pointer;
          border-radius: 100px;
          user-select: none;

          @include _600 {
            width: 80px;
            height: 30px;
            @include font(400, 10px, 11.72px);
          }

          > #icon_messenger1 {
            mask-image: url("../assets/SMS.svg");
          }
          > #icon_messenger2 {
            mask-image: url("../assets/WhatsApp.svg");
          }
          > #icon_messenger3 {
            mask-image: url("../assets/Telegram.svg");
          }

          > div {
            width: 20px;
            height: 20px;
            margin-right: 8px;
            mask-size: 80% 80%;
            mask-repeat: no-repeat;
            mask-position: center center;
            background-color: #8b90a1;

            @include _600 {
              width: 12px;
              height: 12px;
              margin-right: 4px;
            }
          }
        }
        > input {
          display: none;

          color: #ffffff;

          opacity: 0.5;
        }
        > input:checked + label {
          color: #ff00b1;
          background: #101727;

          > div {
            background: #ff00b1;
          }
        }
      }
    }
  }
  > #code {
    width: 360px;
    height: 48px;

    margin: 35px auto 69px;

    background: linear-gradient(90deg, #ff00b1 0%, #b423c1 100%);
    box-shadow: 0px 0px 10px #d70e93;
    border-radius: 4px;
    border: none;

    @include font(700, 15px, 18px);

    text-align: center;
    letter-spacing: 0.05em;
    text-transform: uppercase;

    cursor: pointer;

    color: #ffffff;

    @include _600 {
      width: 240px;
      height: 48px;
      margin: 30px auto 49px;
    }
  }
}
.shortM {
  margin: 9px auto 0px !important;
}
.error_ac {
  border: 1px solid #d13c3c !important;
}
.error {
  display: flex;
  flex-direction: row;
  margin-top: 6px;
  @include _600 {
    display: none;
  }
  #error_logo {
    width: 12px;
    height: 12px;
    margin-right: 5px;
    mask-size: 100% 100%;
    mask-repeat: no-repeat;
    mask-position: center center;
    mask-image: url("../assets/ERROR.svg");
    background-color: #d13c3c;
  }
  .error_number {
    height: 16px;

    @include font(400, 12px, 16px);

    color: #d13c3c;
  }
}
.modal {
  position: fixed;
  width: 100%;
  z-index: 9998;
  top: 112px;
  left: 0;
  margin: 0 auto 0;
  .modal_container {
    display: flex;
    flex-direction: column;
    width: 280px;
    height: 400px;
    margin: 0 auto 0;
    background: #172144;
  }
  .modal_icon {
    width: 80px;
    height: 80px;
    margin: 60px auto 0;
    mask-size: 100% 100%;
    mask-repeat: no-repeat;
    mask-position: center center;
    mask-image: url("../assets/Error_mobile.svg");
    background-color: #ff00b1;
  }
  .modal_name {
    width: 239px;
    height: 20px;
    margin: 30px auto 0;
    @include font(900, 20px, 20px);

    text-align: center;
    text-transform: uppercase;

    color: #ffffff;
  }
  .modal_body {
    width: 238px;
    height: 40px;
    @include font(400, 12px, 20px);
    margin: 15px auto 0;
    text-align: center;

    color: rgba(255, 255, 255, 0.5);
  }
  .modal_btn {
    width: 240px;
    height: 48px;
    @include font(400, 15px, 18px);
    margin: 30px auto 0;
    text-align: center;

    color: #ffffff;
    background: linear-gradient(90deg, #ff00b1 0%, #b423c1 100%);
    box-shadow: 0px 0px 10px #d70e93;
    border-radius: 4px;
    border: none;
  }
}
</style>
