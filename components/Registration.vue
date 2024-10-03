<template lang="pug">
  .flex.column.justify-center.items-center
    span.logo-text LOGO
    span.reg-text Free Registration

    div.q-pa-md
      q-stepper(ref="stepper", v-model="step", color="primary", animated, class="stepper-style")
        q-step(v-for="stepItem in steps", :key="stepItem.name", :name="stepItem.name", :title="stepItem.title")

    div.reg-container
      validation-observer(v-slot="{ handleSubmit, invalid }")
        form(@submit.prevent="handleSubmit(onSubmit)")
          div.q-pa-md
            div.row(style="margin-bottom: 70px")
              div.col-12.text-center(style="height: 100px")
                span.text-white Continue With
                div.row.justify-center.items-center(style="margin-top: 10px")
                  img.icon-image(src="../resources/image/facebook.svg", alt="facebook")
                  img.icon-image(src="../resources/image/google.svg", alt="google")
                div.flex.row.justify-between.items-center(style="margin-top: 40px")
                  hr
                  span.text-white(style="margin: 0 15px") Or
                  hr

            div.row.q-col-gutter-md(style="margin-top: 40px")
              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="username", rules="required|min:6|alpha_dash")
                  label.input-title.text-white Username
                  q-input(v-model="username", class="input-fields", filled, :error="!!errors.length", :error-message="errors[0]", placeholder="Please enter username.")

              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="password", rules="required|min:6")
                  label.input-title.text-white Password
                  q-input(v-model="password", class="input-fields", filled, type="password", :error="!!errors.length", :error-message="errors[0]", placeholder="Please enter password.")

              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="confirmPassword", rules="required|confirmed:password")
                  label.input-title.text-white Confirm Password
                  q-input(v-model="confirmPassword", class="input-fields", filled, type="password", placeholder="Please enter password.", :error="!!errors.length", :error-message="errors[0]")

              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="mobileNumber", rules="required")
                  label.input-title.text-white Mobile Number
                  q-input(v-model="mobileNumber", class="input-fields", type="number", filled, :error="!!errors.length", :error-message="errors[0]", placeholder="Please enter mobile number.")

              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="email", rules="email|required")
                  label.input-title.text-white E-mail Address
                  q-input(v-model="email", class="input-fields", filled, :error="!!errors.length", :error-message="errors[0]", placeholder="Please enter e-mail address.")

              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="idNumber", rules="required")
                  label.input-title.text-white Identity No
                  q-input(v-model="idNumber", class="input-fields", filled, :error="!!errors.length", :error-message="errors[0]", placeholder="Please enter correct ID number.")

              div.col-12.col-sm-6
                label.input-title.text-white Referral
                q-input(v-model="referral", style="color: white", class="input-fields", filled, hint="Leave blank if no referral.", placeholder="Please enter referral username.")
                label.ref-hint Leave blank if no referral.

              div.col-12.col-sm-6
                validation-provider(v-slot="{ errors }", name="verificationCode", :rules="customRule")
                  div.flex.justify-end.items-end
                    div(style="width: 65%")
                      label.input-title.text-white Verification Code
                      q-input(v-model="verificationCode", class="input-fields", filled, :error="!!errors.length", :error-message="errors[0]", placeholder="Verification Code.", style="border-radius: 5px 0 0 5px; background: #262626")

                    div.verification-code
                      span {{ randomNumber }}

              div.col-12.row.items-center.justify-center
                q-checkbox(v-model="agree")
                span.text-white I agree.
                a(href="http://", target="_blank", rel="noopener noreferrer") OCMS Terms & Condition

              div.col-12.row.items-center.justify-center
                q-btn(class="reg-button", color="white", label="Register", type="submit", :disabled="invalid")

</template>

<script>
export default {
data() {
  return {
    step: 1,
    steps: [
      { name: 1, title: "1" },
      { name: 2, title: "2" },
      { name: 3, title: "3" },
    ],
    agree: false,
    username: "",
    password: "",
    confirmPassword: "",
    mobileNumber: "",
    email: "",
    idNumber: "",
    referral: "",
    verificationCode: "",
    randomNumber: null,
  };
},
computed: {
  isValid() {
    return this.model.length <= 3;
  },
  customRule() {
    return "required|is:" + this.randomNumber;
  },
  isAgree() {
    return "is:" + true;
  },
},
mounted() {
  this.generateRandomNumber();
  // console.log(this.randomNumber, 'test')
},

methods: {
  generateRandomNumber() {
    this.randomNumber = Math.floor(Math.random() * (9999 - 1000 + 1)) + 1000;
  },
  onSubmit() {
      console.log("Form Submitted:", {
      agree: this.agree,
      username: this.username,
      password: this.password,
      confirmPassword: this.confirmPassword,
      mobileNumber: this.mobileNumber,
      email: this.email,
      idNumber: this.idNumber,
      referral: this.referral,
      verificationCode: this.verificationCode,
    });
  },
},
};
</script>

<style>
.reg-container {
height: 831px;
width: 760px;
background: #000000;
border: 2px #ffcc00 solid;
border-radius: 8px;
padding: 47px;
}

.reg-text {
color: #ffff00;
margin-bottom: 30px;
margin-top: 20px;
font-size: 2.5rem;
font-weight: 700;
color: #ffff;
}

.logo-text {
color: #ffff00;
margin-top: 56px;
font-size: 3.125rem;
font-weight: 700;
}

.reg-button {
background: linear-gradient(
  to bottom,
  rgba(234, 159, 19, 1) 0%,
  rgba(234, 159, 19, 1) 50%,
  rgba(187, 127, 15, 1) 100%
) !important;
border: 2px rgba(187, 127, 15, 1) solid;
border-radius: 50px;
width: 160px;
height: 54px;
box-shadow: 0px 6px 0px 0px #ffffff40 inset;
color: #ffffff !important;
text-transform: capitalize;
}

a {
color: #d99e30;
text-decoration: none;
}

hr {
width: 270px;
margin: 0;
border: 1px #808080 solid;
}

.input-fields {
height: 65px;
border-radius: 5px;
color: #b0b0b0 !important;
background: #262626;

::placeholder {
  color: #b0b0b0;
}
}

.q-field__native {
color: #808080;
}

.input-title {
font-size: 15px;
line-height: 30px;
}

.material-icons {
display: none;
}

.q-field__control {
height: 50px;
}

.q-field__bottom {
margin-bottom: 5px;
}

.icon-image {
height: 50px;
width: 50px;
}

.google-icon {
border-radius: 5px;
margin-left: 20px;
background: #ffff;
}

.q-checkbox__append {
display: flex;
align-items: center;
}

/* stepper css */
.q-stepper__tab--active .q-stepper__dot {
background: #eb9f13;
height: 70px;
width: 70px;
}

.q-stepper__dot {
background: #000000;
height: 50px;
width: 50px;
}

.q-stepper {
box-shadow: none;
margin-bottom: 20px;
}

.q-stepper__header {
border: 0;
}

.q-stepper__tab {
justify-content: center;
}

.q-stepper__label {
right: 44px;
color: #ffffff;
}

.q-stepper__tab--active .q-stepper__label {
right: 55px;
color: #ffffff;
}

.q-stepper__title {
font-size: 2.5rem;
}

.q-stepper--horizontal .q-stepper__line:before {
height: 4px;
background: #47576e;
margin-right: 10px;
}

.q-stepper--horizontal .q-stepper__line:after {
height: 4px;
background: #47576e;
margin-left: 35px;
}

.ref-hint {
color: #959595;
font-size: 14px;
font-weight: 400;
line-height: 16.94px;
}

.q-checkbox__bg {
background: #ffffff;
}
.verification-code {
width: 35%;
height: 68px;
background: #ffff;
border-radius: 0 5px 5px 0;
display: flex;
align-items: center;
justify-content: center;
font-size: 1.3rem;
color: red;
}
.stepper-style {
width: 500px;
background: none;
}

@media only screen and (max-width: 600px) {
html,
body {
  height: 1900px !important;
}
.reg-container {
  height: 1250px;
  width: 355px;
  padding: 0 22px;
}
hr {
  width: 110px;
}
.stepper-style {
  width: 450px;
  background: none;
}
}
</style>
