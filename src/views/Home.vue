<template>
  <div class="paymentpage">
    <div class="container">
      <div class="payment">
        <div class="payment__nav">
          <div
            class="payment__nav__item"
            :class="
              step === 1
                ? 'payment__nav__item--active'
                : '' || step === 2
                ? 'payment__nav__item--active'
                : '' || step === 3
                ? 'payment__nav__item--active'
                : ''
            "
          >
            <div class="payment__nav__item__number">1</div>
            <div class="payment__nav__item__text">Delivery</div>
          </div>
          <div
            class="payment__nav__item"
            :class="
              step === 2
                ? 'payment__nav__item--active'
                : '' || step === 3
                ? 'payment__nav__item--active'
                : ''
            "
          >
            <div class="payment__nav__item__number">2</div>
            <div class="payment__nav__item__text">Payment</div>
          </div>
          <div
            class="payment__nav__item"
            :class="step === 3 ? 'payment__nav__item--active' : ''"
          >
            <div class="payment__nav__item__number">3</div>
            <div class="payment__nav__item__text">Finish</div>
          </div>
        </div>
        <div class="payment__bg-box">
          <section v-if="step == 1">
            <div class="payment-content">
              <div class="payment-content__back">
                <a href="">
                  <ArrowLeft />
                  Back to cart
                </a>
              </div>
              <div class="payment-content__container">
                <div class="payment-content__left">
                  <div class="payment-content__left__top">
                    <h1>Delivery details</h1>
                    <div class="form">
                      <label for="asDropshipper" class="checkmark">
                        <input
                          type="checkbox"
                          id="asDropshipper"
                          v-model="asDropshipper"
                          class="checkmark__input"
                        />
                        <span class="checkmark__label"
                          >Send as dropshipper</span
                        >
                      </label>
                    </div>
                  </div>
                  <div class="payment-content__left__bottom">
                    <div class="payment-content__left__row">
                      <div class="payment-content__left__row__left">
                        <div :class="['form-group', isEmailValid()]">
                          <label
                            for=""
                            class="form-group__label"
                            :class="
                              form.email
                                ? 'active'
                                : '' || formFocusEmail
                                ? 'active'
                                : ''
                            "
                            >Email</label
                          >
                          <input
                            placeholder="Email"
                            type="email"
                            v-model="form.email"
                            class="form-group__input"
                            @focus="setFocusEmail"
                            @blur="removeFocusEmail"
                            :class="
                              form.email
                                ? 'active'
                                : '' || formFocusEmail
                                ? 'active'
                                : ''
                            "
                          />
                        </div>

                        <div :class="['form-group', isPhoneValid()]">
                          <label
                            class="form-group__label"
                            :class="
                              form.phone
                                ? 'active'
                                : '' || formFocusPhone
                                ? 'active'
                                : ''
                            "
                            >Phone Number</label
                          >
                          <input
                            placeholder="Phone Number"
                            type="text"
                            v-model="form.phone"
                            class="form-group__input"
                            @focus="setFocusPhone"
                            @blur="removeFocusPhone"
                            :class="
                              form.phone
                                ? 'active'
                                : '' || formFocusPhone
                                ? 'active'
                                : ''
                            "
                            v-on:keypress="onlyNumber"
                            maxlength="20"
                          />
                        </div>
                        <div :class="['form-group', isAddressValid()]">
                          <label
                            for=""
                            class="form-group__label"
                            :class="
                              form.address
                                ? 'active'
                                : '' || formFocusAddress
                                ? 'active'
                                : ''
                            "
                            >Delivery Address</label
                          >
                          <textarea
                            placeholder="Delivery Address"
                            maxlength="120"
                            v-model="form.address"
                            class="form-group__input form-group__input--height"
                            @focus="setFocusAddress"
                            @blur="removeFocusAddress"
                            :class="
                              form.address
                                ? 'active'
                                : '' || formFocusAddress
                                ? 'active'
                                : ''
                            "
                            @input="calcMax"
                          ></textarea>
                          <span class="addressLength"
                            >Maksimum : {{ maxAddress }}</span
                          >
                        </div>
                      </div>
                      <!-- dropshiper -->
                      <div class="payment-content__left__row__right">
                        <div :class="['form-group', isDropNameValid()]">
                          <label
                            for=""
                            class="form-group__label"
                            :class="
                              form.dropName
                                ? 'active'
                                : '' || formFocusDropName
                                ? 'active'
                                : ''
                            "
                            >Dropshipper name</label
                          >
                          <input
                            type="text"
                            placeholder="Dropshipper name"
                            v-model="form.dropName"
                            class="form-group__input"
                            :disabled="!asDropshipper"
                            @focus="setFocusDropName"
                            @blur="removeFocusDropName"
                            :class="
                              form.dropName
                                ? 'active'
                                : '' || formFocusDropName
                                ? 'active'
                                : ''
                            "
                          />
                        </div>
                        <div :class="['form-group', isDropPhoneValid()]">
                          <label
                            for=""
                            class="form-group__label"
                            :class="
                              form.dropPhone
                                ? 'active'
                                : '' || formFocusDropPhone
                                ? 'active'
                                : ''
                            "
                            >Dropshipper phone number</label
                          >
                          <input
                            type="text"
                            placeholder="Dropshipper phone number"
                            v-model="form.dropPhone"
                            class="form-group__input"
                            :disabled="!asDropshipper"
                            @focus="setFocusDropPhone"
                            @blur="removeFocusDropPhone"
                            :class="
                              form.dropPhone
                                ? 'active'
                                : '' || formFocusDropPhone
                                ? 'active'
                                : ''
                            "
                            v-on:keypress="onlyNumber"
                            maxlength="20"
                          />
                        </div>
                      </div>
                    </div>
                  </div>
                  <span class="errorText" :v-if="errorText">{{errorText}}</span>
                </div>
                <!-- summary -->
                <div class="payment-content__right">
                  <div class="payment-content__right__top">
                    <h3>Summary</h3>
                    <div class="tot-item">
                      {{ form.totalItem }} Items purchased
                    </div>
                  </div>
                  <div class="payment-content__right__bottom">
                    <div class="detail-items">
                      <div class="detail-items__item">
                        <div class="title">Cost of goods</div>
                        <div class="price">
                          {{ form.harga | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item" v-if="asDropshipper">
                        <div class="title">Dropshipper Fee</div>
                        <div class="price">
                          {{ dropshipperFee | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item detail-items__item--total">
                        <div class="title">Total</div>
                        <div class="price">
                          {{ totalHarga | currency("", 0) }}
                        </div>
                      </div>
                    </div>
                    <button
                      class="button-next"
                      v-if="step != totalStep"
                      @click="nextStep"
                    >
                      Continue to Payment
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </section>
          <!-- step 2 -->
          <section v-if="step == 2">
            <div class="payment-content">
              <div class="payment-content__back">
                <a @click.prevent="prevStep">
                  <ArrowLeft />
                  Back to delivery
                </a>
              </div>
              <div class="payment-content__container">
                <div class="payment-content__left">
                  <h1 class="mb-30">Shipment</h1>
                  <div class="payment-content__left__row align-center mb-60 flex-wrap">
                    <div
                      class="form-group form-select"
                      v-for="item in shipmentList"
                      :key="item.id"
                    >
                      <input
                        class="form-group__input-radio"
                        type="radio"
                        :id="item.name"
                        :value="item.name"
                        v-model="form.shipment"
                        @change="checkShipment"
                      />
                      <label class="form-group__label-radio" :for="item.name">
                        <div class="text">
                          {{ item.name }}
                        </div>
                        <div class="price">
                          {{ item.price | currency("", 0) }}
                        </div>
                      </label>
                    </div>
                  </div>

                  <h1 class="mb-30">Payment</h1>
                  <div class="payment-content__left__row align-center mb-60">
                    <div
                      class="form-group form-select"
                      v-for="itemPay in paymentList"
                      :key="itemPay.id"
                    >
                      <input
                        class="form-group__input-radio"
                        type="radio"
                        :id="itemPay.name"
                        :value="itemPay.name"
                        v-model="form.payment"
                      />
                      <label
                        class="form-group__label-radio"
                        :for="itemPay.name"
                      >
                        <div
                          class="text"
                          :class="
                            itemPay.name === 'Bank Transfer'
                              ? 'big'
                              : '' || itemPay.name === 'Virtual Account'
                              ? 'big'
                              : ''
                          "
                        >
                          {{ itemPay.name }}
                        </div>
                        <div class="price">
                          {{ itemPay.price }}
                        </div>
                      </label>
                    </div>
                  </div>
                  <span class="errorText" :v-if="errorText">{{errorText}}</span>
                </div>
                <div class="payment-content__right">
                  <div class="payment-content__right__top">
                    <h3>Summary</h3>
                    <div class="tot-item">
                      {{ form.totalItem }} Items purchased
                    </div>
                    <div class="divider"></div>
                    <div class="deliv-estimation" v-if="form.shipment">
                      <div class="deliv-estimation__label">
                        Delivery estimation
                      </div>
                      <div class="delive-estimation__select">
                        {{ form.shipmentEstimate }} by {{ form.shipment }}
                      </div>
                    </div>
                  </div>
                  <div class="payment-content__right__bottom">
                    <div class="detail-items">
                      <div class="detail-items__item">
                        <div class="title">Cost of goods</div>
                        <div class="price">
                          {{ form.harga | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item" v-if="asDropshipper">
                        <div class="title">Dropshipper Fee</div>
                        <div class="price">
                          {{ dropshipperFee | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item" v-if="form.shipmentFee">
                        <div class="title">
                          <b>{{ form.shipment }}</b> shipment
                        </div>
                        <div class="price">
                          {{ form.shipmentFee | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item detail-items__item--total">
                        <div class="title">Total</div>
                        <div class="price">
                          {{ totalHarga | currency("", 0) }}
                        </div>
                      </div>
                    </div>
                    <button
                      class="button-next"
                      v-if="step != totalStep"
                      @click="nextStep"
                    >
                      Continue to Payment
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </section>
          <section v-if="step == 3">
            <div class="payment-content">
              <div class="payment-content__container">
                <div class="payment-content__left">
                  <div
                    class="
                      payment-content__left__row
                      align-center
                      justify-center
                      height-100
                    "
                  >
                    <div class="payment-content__left__row__thanks">
                      <div class="thankyou mb-60">
                        <h1 class="mb-30">Thank you</h1>
                        <div class="thankyou__id">
                          Order ID : {{ form.orderID | uppercase }}
                        </div>
                        <p class="thankyou__shipment">
                          Your order will be delired
                          {{ form.shipmentEstimate }} with {{ form.shipment }}
                        </p>
                      </div>
                      <div class="payment-content__back">
                        <a @click.prevent="removeLocalStorage">
                          <ArrowLeft />
                          Go to homepage
                        </a>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="payment-content__right">
                  <div class="payment-content__right__top">
                    <h3>Summary</h3>
                    <div class="tot-item">
                      {{ form.totalItem }} Items purchased
                    </div>
                    <div class="divider"></div>
                    <div class="deliv-estimation" v-if="form.shipment">
                      <div class="deliv-estimation__label">
                        Delivery estimation
                      </div>
                      <div class="delive-estimation__select">
                        {{ form.shipmentEstimate }} by {{ form.shipment }}
                      </div>
                    </div>
                    <div class="divider"></div>
                    <div class="deliv-estimation" v-if="form.payment">
                      <div class="deliv-estimation__label">Payment method</div>
                      <div class="delive-estimation__select">
                        {{ form.payment }}
                      </div>
                    </div>
                  </div>
                  <div class="payment-content__right__bottom">
                    <div class="detail-items">
                      <div class="detail-items__item">
                        <div class="title">Cost of goods</div>
                        <div class="price">
                          {{ form.harga | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item" v-if="asDropshipper">
                        <div class="title">Dropshipper Fee</div>
                        <div class="price">
                          {{ dropshipperFee | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item" v-if="form.shipmentFee">
                        <div class="title">
                          <b>{{ form.shipment }}</b> shipment
                        </div>
                        <div class="price">
                          {{ form.shipmentFee | currency("", 0) }}
                        </div>
                      </div>
                      <div class="detail-items__item detail-items__item--total">
                        <div class="title">Total</div>
                        <div class="price">
                          {{ totalHarga | currency("", 0) }}
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ArrowLeft from "vue-material-design-icons/ArrowLeft.vue";

export default {
  name: "Home",
  components: {
    ArrowLeft,
    //Check,
    //Clear
  },
  data() {
    return {
      totalStep: 3,
      step: 1,
      btnNext: false,
      form: {
        email: "",
        phone: "",
        address: "",
        dropName: "",
        dropPhone: "",
        totalItem: 10,
        harga: 500000,
        hargaTotal: 500000,
        shipment: "",
        shipmentFee: "",
        shipmentEstimate: "",
        payment: "",
        orderID: "",
      },
      shipmentList: [
        {
          id: 1,
          name: "GO-SEND",
          price: 15000,
        },
        {
          id: 2,
          name: "JNE",
          price: 9000,
        },
        {
          id: 3,
          name: "Personal Courier",
          price: 29000,
        },
      ],
      paymentList: [
        {
          id: 100,
          name: "e-Wallet",
          price: "1500000 left",
        },
        {
          id: 101,
          name: "Bank Transfer",
          price: "",
        },
        {
          id: 102,
          name: "Virtual Account",
          price: "",
        },
      ],
      eWallet: 1500000,
      maxAddress: 120,
      regEmail:
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
      asDropshipper: false,
      dropshipperFee: 5900,
      formFocusPhone: false,
      formFocusEmail: false,
      formFocusAddress: false,
      formFocusDropName: false,
      formFocusDropPhone: false,
      errorText: '',
    };
  },
  mounted() {
    if (JSON.parse(window.localStorage.getItem('form'))) {
      let data = JSON.parse(window.localStorage.getItem('form'))
      this.form = data;
      this.step = localStorage.step
      this.form.orderID = localStorage.orderId
    }
  },
  //watch: {
  //  step(val){
  //    localStorage.step = val;  
  //  },
  //},
  computed: {
    totalHarga: function () {
      if (this.asDropshipper) {
        return this.form.harga + this.dropshipperFee + this.form.shipmentFee;
      } else {
        return this.form.harga + this.form.shipmentFee;
      }
    },
  },
  methods: {
    randomOrderId: function () {
      if (this.step == 3) {
        let text = "";
        let chars = "abcdefghijkmnpqrstuvwxyz23456789";
        let length = 5;
        for (let x = 0; x < length; x++) {
          text += chars.charAt(
            Math.floor(Math.random() * chars.length)
          );
        }
        this.form.orderID = text
        window.localStorage.setItem('orderId', this.form.orderID);
      }
    },
    nextStep: function () {
      if (this.step == 1) {
        if (!this.form.email) {
          this.errorText = '*the fields is required'
          return false;
        } else if (!this.form.phone) {
          this.errorText = '*the fields is required'
          return false;
        } else if (!this.form.address) {
          this.errorText = '*the fields is required'
          return false;
        } else if (this.asDropshipper) {
          if (!this.form.dropName) {
            this.errorText = '*the fields is required'
            return false;
          } else if (!this.form.dropPhone) {
            this.errorText = '*the fields is required'
            return false;
          } else if (document.querySelector(".error")) {
            this.errorText = '*please check the fields'
            return false;
          }
        } else if (document.querySelector(".error")) {
          this.errorText = '*please check the fields'
          return false;
        }
      }
      if (this.step == 2) {
        if (!this.form.shipment) {
          this.errorText = '*the fields is required'
          return false;
        } else if (!this.form.payment) {
          this.errorText = '*the fields is required'
          return false;
        }
      }
      let data = JSON.stringify(this.form)
      this.errorText = ''
      window.localStorage.setItem('form', data);
      this.step++;
      this.randomOrderId();
      localStorage.step = this.step;
    },
    prevStep: function () {
      this.step--;
    },
    setFocusPhone: function () {
      this.formFocusPhone = true;
    },
    removeFocusPhone: function () {
      this.formFocusPhone = false;
    },
    setFocusEmail: function () {
      this.formFocusEmail = true;
    },
    removeFocusEmail: function () {
      this.formFocusEmail = false;
    },
    setFocusAddress: function () {
      this.formFocusAddress = true;
    },
    removeFocusAddress: function () {
      this.formFocusAddress = false;
    },
    setFocusDropName: function () {
      this.formFocusDropName = true;
    },
    removeFocusDropName: function () {
      this.formFocusDropName = false;
    },
    setFocusDropPhone: function () {
      this.formFocusDropPhone = true;
    },
    removeFocusDropPhone: function () {
      this.formFocusDropPhone = false;
    },
    isEmailValid: function () {
      return this.form.email == ""
        ? ""
        : this.regEmail.test(this.form.email)
        ? "valid"
        : "error";
    },
    isPhoneValid: function () {
      return this.form.phone == ""
        ? ""
        : this.form.phone.length > 5 && this.form.phone.length < 21
        ? "valid"
        : "error";
    },
    onlyNumber: function (evt) {
      evt = evt ? evt : window.event;
      var charCode = evt.which ? evt.which : evt.keyCode;
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46
      ) {
        evt.preventDefault();
      } else {
        return true;
      }
    },
    isAddressValid: function () {
      return this.form.address == ""
        ? ""
        : this.form.address.length > 1 && this.form.phone.length < 121
        ? "valid"
        : "error";
    },
    calcMax: function () {
      this.maxAddress = 120 - this.form.address.length;
    },
    isDropNameValid: function () {
      return this.form.dropName == ""
        ? ""
        : this.form.dropName.length > 0
        ? "valid"
        : "error";
    },
    isDropPhoneValid: function () {
      return this.form.dropPhone == ""
        ? ""
        : this.form.dropPhone.length > 5 && this.form.dropPhone.length < 21
        ? "valid"
        : "error";
    },
    checkShipment: function () {
      if (this.form.shipment == "GO-SEND") {
        this.form.shipmentFee = 15000;
        this.form.shipmentEstimate = "today";
      } else if (this.form.shipment == "JNE") {
        this.form.shipmentFee = 9000;
        this.form.shipmentEstimate = "2 days";
      } else {
        this.form.shipmentFee = 29000;
        this.form.shipmentEstimate = "1 day";
      }
    },
    removeLocalStorage: function(){
      localStorage.removeItem('form');
      localStorage.removeItem('step');
      localStorage.removeItem('orderId');
      location.reload();
    }
  },
};
</script>
<style lang="stylus" scoped>
@import './../assets/style/variable.styl';

.payment__nav {
  z-index: 1;
  position: relative;
  display: flex;
  align-items: center;
  padding: 20px 38px;
  border-radius: 35px;
  background: color-orange-bg;
  margin: 0 auto;
  margin-top: 20px;
  width: fit-content;
  @media screen and (max-width: 767px){
    padding : 16px
    border-radius: 30px;
  }
}

.payment__nav__item {
  display: flex;
  align-items: center;
  margin-right: 21px;
  padding-right: 22px;
  position: relative;
  @media screen and (max-width: 767px){
    font-size : 12px
    margin-right: 15px;
    padding-right: 15px;
  }

  &:after {
    position: absolute;
    content: '>';
    right: 0;
    top: 50%;
    transform: translateY(-50%);
    color: color-orange;
    @media screen and (max-width: 767px){
      font-size : 12px
    }
  }

  &:last-child {
    margin-right: 0;
    padding-right: 0;

    &:after {
      content: '';
    }
  }
}

.payment__nav__item__number {
  line-height: 19px;
  margin-right: 10px;
  color: color-orange;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: rgba(255, 138, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
  @media screen and (max-width: 767px){
    width : 18px
    height : 18px
    font-size : 12px
  }
}

.payment__nav__item__text {
  color: color-orange;
}

.payment__nav__item--active {
  .payment__nav__item__number {
    color: white;
    background: color-orange;
  }
}

.payment__bg-box {
  margin-top: -35px;
  z-index: -1;
  //width: 100%;
  height: auto;
  background: white;
  box-shadow: 2px 10px 20px rgba(255, 138, 0, 0.1);
  border-radius: 4px;
  padding: 30px 20px 20px 40px;
  @media screen and (max-width: 768px){
    margin-top : -15px
    padding : 20px
    padding-top : 30px
  }
}

.payment-content__back {
  a {
    display: flex;
    align-items: center;
    color: color-black;
    transition: 0.3s;
    cursor: pointer;

    span {
      color: color-black;
      margin-right: 10px;
      display: flex;
      align-items: center;
      transition: 0.3s;
    }
  }

  &:hover {
    a, span {
      color: color-orange;
    }
  }
}

.payment-content__container {
  margin-top: 24px;
  display: flex;
  @media screen and (max-width: 768px){
    flex-wrap : wrap
  }
}

.payment-content__left {
  flex: 1;
  min-height: 460px;
  @media screen and (max-width: 768px){
    width : 100%
    min-height: 310px;
  }
}

.payment-content__left__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-right: 57px;
  @media screen and (max-width: 768px){
    flex-wrap : wrap
  }
}

.payment-content__left__bottom {
  margin-top: 36px;
}

.payment-content__right {
  //width: 280px;
  width: 27%
  @media screen and (max-width: 768px){
    width : 100%
    margin-top : 20px
  }
}

.payment-content__left__row {
  display: flex;
  margin-right: 30px;
  @media screen and (max-width: 768px){
    flex-wrap : wrap
    margin-right: 0;
  }
}

.payment-content__left__row__left {
  width: 57%;
  margin-right: 3%;
  @media screen and (max-width: 768px){
    width : 100%
    margin-right : 0
  }
}

.payment-content__left__row__right {
  width: 40%;
  @media screen and (max-width: 768px){
    width : 100%
    margin-top : 20px
  }
}

.addressLength {
  position: absolute;
  right: 0;
  color: color-gray;
  font-size: 12px;
}

// summary
.payment-content__right {
  border-left: 1px solid rgba(255, 138, 0, 0.2);
  padding-left: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.payment-content__right__top {
  .tot-item {
    color: black;
    font-size: 14px;
    line-height: 17px;
    font-weight: normal;
    margin-top: 10px;
    opacity: 0.6;
  }
}

.detail-items {
  margin-bottom: 30px;
}

.detail-items__item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;

  &:last-child {
    margin-bottom: 0;
  }

  .title {
    font-weight: normal;
    font-size: 14px;
    line-height: 17px;
    color: black;
    opacity: 0.6;
  }

  .price {
    font-weight: bold;
    font-size: 14px;
    line-height: 17px;
    color: black;
  }

  &.detail-items__item--total {
    .title, .price {
      opacity: 1;
      font-family: Montserrat-Bold;
      color: color-orange;
      font-size: 24px;
      line-height: 29px;
    }
  }
}

.button-next {
  width: 100%;
  border: 0;
  padding: 20px 8px;
  text-align: center;
  font-weight: 500;
  font-size: 18px;
  line-height: 22px;
  color: white;
  background: color-orange;
  cursor: pointer;
  transition: 0.3s;

  &.disable {
    background: color-gray;

    &:hover {
      cursor: no-drop;
    }
  }

  &:hover {
    box-shadow: 1px 2px 8px #00000042;
  }
}

.deliv-estimation__label {
  color: black;
  font-size: 14px;
  line-height: 17px;
  margin-bottom: 4px;
}

.delive-estimation__select {
  color: color-green;
}

.thankyou__id {
  font-size: 14px;
  line-height: 17px;
  color: black;
}

.thankyou__shipment {
  font-size: 14px;
  line-height: 17px;
  color: black;
  opacity: 0.6;
  margin-top: 10px;
}
</style>
