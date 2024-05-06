<script setup>
import { ref } from 'vue'
import { Form, Field, ErrorMessage } from 'vee-validate';
import * as yup from 'yup';
import Swal from 'sweetalert2';

const passwordIsVisible = ref(true)
const confirmIsVisible = ref(true)

const schema = yup.object({
  fullName: yup.string()
    .matches(/^[A-Za-z\u4e00-\u9fff]+$/, '輸入只能是中文或英文')
    .required('此欄位為必填'),
  email: yup.string()
    .matches(/^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/, '請輸入有效的電子郵件')
    .required('此欄位為必填'),
  phoneNumber: yup.string()
    .matches(/^(0[2-9]|[1-9][0-9]|1[0-9]{2})(?:-)?[0-9]{8}$/, '請輸入包含區碼的號碼').required('此欄位為必填'),
  username: yup.string()
    .matches(/^(0[2-9]|[1-9][0-9]|1[0-9]{2})[0-9]{8}$/, '請輸入有效的手機號碼').required('此欄位為必填'),
  password: yup.string()
    .matches(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{6,12}$/, '密碼須包含大小寫及數字').required('此欄位為必填'),
  confirmPassword: yup.string()
    .required('此欄位為必填')
    .oneOf([yup.ref('password')], '密碼不相符'),
  pets: yup.string().required('此欄位為必填')
});

function formatDetails(details) {
  let formattedDetails = '';
  for (const key in details) {
    if (details.hasOwnProperty(key)) {
      // 將屬性值轉換成字符串，並根據屬性類型進行格式化
      const value = typeof details[key] === 'string'? `"${details[key]}"` : details[key];
      formattedDetails += `${key}: ${value}, `;
    }
  }
  // 移除最後一個逗號和空格
  return formattedDetails.slice(0, -2);
}

function onSubmit(values) {
  const details = {
    fullName: values.fullName,
    email: values.email,
    phoneNumber: values.phoneNumber,
    username: values.username,
    pets: values.pets,
    otherPets: values.otherPets? values.otherPets : null,
    password: values.password,
    confirmPassword: values.confirmPassword,
  }
  Swal.fire({
    title: '註冊成功!',
    text: formatDetails(details),
    icon: 'success',
    confirmButtonText: 'OK!'
  });
}

function toggleVisibility(e) {
  if(e.target.previousElementSibling.type === 'password'){
    e.target.previousElementSibling.type = "text"
    passwordIsVisible.value = false
  } else if(e.target.previousElementSibling.type === 'text') {
    e.target.previousElementSibling.type = "password"
    passwordIsVisible.value = true
  }
}

function toggleConfirmVisibility(e) {
  if(e.target.previousElementSibling.type === 'password'){
    e.target.previousElementSibling.type = "text"
    confirmIsVisible.value = false
  } else if(e.target.previousElementSibling.type === 'text') {
    e.target.previousElementSibling.type = "password"
    confirmIsVisible.value = true
  }
}



</script>

<template>
  <div class="container">
    <h1 class="form-title">會員註冊</h1>
    <Form :validation-schema="schema" @submit="onSubmit">
      <div class="main-user-info">
        
        <div class="user-input-box">
          <label for="fullName">姓名</label>
          <Field type="text" name="fullName" id="fullName" placeholder="請輸入中文或英文姓名" />
          <ErrorMessage name="fullName" class="errorMessage"/>
        </div>

        <div class="user-input-box">
          <label for="email">電子郵件</label>
          <Field type="text" name="email" id="email" placeholder="請輸入電子郵件" />
          <ErrorMessage name="email" class="errorMessage"/>
        </div>
        
        <div class="user-input-box">
          <label for="phoneNumber">電話號碼</label>
          <Field type="text" name="phoneNumber" id="phoneNumber" placeholder="請輸入包含區碼的電話號碼" />
          <ErrorMessage name="phoneNumber" class="errorMessage"/>
        </div>

        <div class="user-input-box">
          <label for="username">帳號</label>
          <Field type="text" name="username" id="username" placeholder="請輸入手機號碼" />
          <ErrorMessage name="username" class="errorMessage"/>
        </div>

        <div class="user-input-box">
          <label for="password">密碼</label>
          <div class="input-field">
            <Field type="password" name="password" id="password" placeholder="密碼須包含大小寫英文及數字"/>
            <span v-if="passwordIsVisible" class="material-symbols-outlined " @click="toggleVisibility">visibility</span>
            <span v-else class="material-symbols-outlined" @click="toggleVisibility">visibility_off</span>
          </div>
          <ErrorMessage name="password" class="errorMessage"/>
        </div>

        <div class="user-input-box">
          <label for="confirmPassword">確認密碼</label>
          <div class="input-field">
            <Field type="password" name="confirmPassword" id="confirmPassword" placeholder="請再次輸入密碼"/>
            <span v-if="confirmIsVisible" class="material-symbols-outlined " @click="toggleConfirmVisibility">visibility</span>
            <span v-else class="material-symbols-outlined" @click="toggleConfirmVisibility">visibility_off</span>
          </div>
          <ErrorMessage name="confirmPassword" class="errorMessage"/>
        </div>

      </div>
      <div class="user-details">
        <span class="pets">已經有養寵物嗎?</span>
        <ErrorMessage name="pets" class="errorMessage" />
        <div class="pets-category">
          <Field type="radio" name="pets" id="cat" value="cat"/>
          <label for="cat">貓</label>
          <Field type="radio" name="pets" id="dog" value="dog"/>
          <label for="dog">狗</label>
          <Field type="radio" name="pets" id="noPets" value="noPets"/>
          <label for="noPets">無</label>
          <Field type="radio" name="pets" id="other" value="other"/>
          <label for="other">其他</label>
        </div>
        <Field as="textarea" name="otherPets" id="otherPets" rows="4" placeholder="你養了甚麼特別的寵物?"></Field>
      </div>

      <div class="form-submit-btn">
        <button type="submit" class="submit-btn">註冊</button>
        <button type="reset" class="reset-btn">重填</button>
      </div>
    </Form>
  </div>
</template>

<style scope>
  .container {
    width: 100%;
    max-width: 650px;
    padding: 28px;
    margin: 0 28px;
    border-radius: 10px;
    background: rgba(0,0,0,0.5);
  }

  .form-title {
    font-size: 35px;
    font-weight: 600;
    text-align: center;
    text-shadow: 1px 1px 1px black;
    color: white;
    padding-bottom: 6px;
    border-bottom: solid 1px white;
  }

  .main-user-info {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 20px 0;
  }

  .user-input-box {
    display: flex;
    flex-wrap: wrap;
    width: 45%;
    padding-bottom: 15px;
  }

  .user-input-box:nth-child(2n) {
    justify-content: end;
  } 

  .user-input-box label {
    width: 95%;
    margin: 5px 0;
    color: white;
  }

  .user-input-box input {
    width: 95%;
    height: 45px;
    padding: 5px 15px 5px 5px;
    border-radius: 8px;
    border: 0;
    outline: 0;
    background-color: #f2f2f2e6;
    font-size: 0.8rem;
  }

  .input-field {
    position: relative;
    width: 100%;
  }

  .user-details {
    color: white
  }

  .pets-category {
    margin: 15px 0;
  }

  .pets-category label {
    padding: 0 20px 0 5px;
  }

  .pets-category label,
  .pets-category input,
  .form-submit-btn button {
    cursor: pointer;
    font-size: 0.8rem;
  }

  input[type="radio"] {
    -ms-transform: scale(2); /* IE 9 */
    -webkit-transform: scale(2); /* Chrome, Safari, Opera */
    transform: scale(2);
  }

  textarea {
    background-color: #f2f2f2e6;
    outline: 0;
    padding: 5px;
    font-size: 0.8rem;
    width: 100%; /* 設置寬度為100%，使其佔滿父元素的全部寬度 */
    height: 100%; /* 設置高度為100%，使其佔滿父元素的全部高度 */
    resize: none; 
  }

  .form-submit-btn{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 100%;
    margin-top: 15px;
  }

  .form-submit-btn button {
    width: 48%;
    font-size: 20px;
    color: rgb(209, 209, 209);
    padding: 8px;
    border: 0;
  }

  .submit-btn {
    background-color: rgba(63, 114, 76, 0.7);
  }
  .submit-btn:hover {
    background-color: rgba(50, 121, 68, 0.9);
  }

  .reset-btn {
    background-color: rgba(181, 71, 55, 0.7);
  }
  .reset-btn:hover {
    background-color: rgba(181, 71, 55, 0.9);
  }

  .errorMessage {
    width: 95%;
    color:rgb(190, 28, 3);
    font-size: 0.8rem;
    font-weight: 600;
  }

  .material-symbols-outlined {
    position: absolute;
    top: 50%;
    right: 25px;
    transform: translateY(-50%);
  }
  
  @media screen and (max-width: 600px) {
    .container {
      min-width: 280px;
    }

    .user-input-box {
      margin-bottom: 12px;
      width: 100%;
    }

    .user-input-box:nth-child(2n) {
      justify-content: space-between;
    } 

    .pets-category {
      display: flex;
      justify-content: space-between;
      width: 100%;
    }

    .form-submit-btn button {
      width: 100%;
      margin-bottom: 10px;
    }

  }

</style>
