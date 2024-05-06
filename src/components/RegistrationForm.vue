<template>
  <div class="container">
    <h1 class="form-title">會員註冊</h1>
    <form>
      <div class="main-user-info">
        
        <div class="user-input-box">
          <label for="fullName">姓名</label>
          <input type="text" name="fullName" id="fullName" placeholder="請輸入全名">
        </div>

        <div class="user-input-box">
          <label for="email">電子郵件</label>
          <input type="text" name="email" id="email" placeholder="請輸入電子郵件">
        </div>
        
        <div class="user-input-box">
          <label for="phoneNumber">電話號碼</label>
          <input type="text" name="phoneNumber" id="phoneNumber" placeholder="請輸入電話號碼">
        </div>

        <div class="user-input-box">
          <label for="username">帳號</label>
          <input type="text" name="username" id="username" placeholder="請輸入手機號碼">
        </div>

        <div class="user-input-box">
          <label for="password">密碼</label>
          <input type="password" name="password" id="password" placeholder="請輸入密碼">
        </div>

        <div class="user-input-box">
          <label for="confirmPassword">確認密碼</label>
          <input type="password" name="confirmPassword" id="confirmPassword" placeholder="請再次輸入密碼">
        </div>

      </div>
      <div class="user-details">
        <span class="pets">你有養寵物嗎?</span>
        <div class="pets-category">
          <input type="radio" name="pets" id="cat">
          <label for="cat">貓</label>
          <input type="radio" name="pets" id="dog">
          <label for="dog">狗</label>
          <input type="radio" name="pets" id="noPets">
          <label for="noPets">無</label>
          <input type="radio" name="pets" id="other">
          <label for="other">其他</label>
        </div>
        <textarea name="otherPets" id="otherPets" rows="4" cols="25" placeholder="你養了甚麼特別的寵物?"></textarea>
      </div>

      <div class="form-submit-btn">
        <input type="submit" value="註冊" class="submit-btn">
        <input type="reset" value="重填" class="reset-btn">
      </div>
    </form>
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
    padding: 5px 10px;
    border-radius: 8px;
    border: 0;
    outline: 0;
    background-color: #f2f2f2e6
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
  .form-submit-btn input {
    cursor: pointer;
  }

  textarea {
    background-color: #f2f2f2e6;
    outline: 0;
    padding: 5px;
  }

  .form-submit-btn{
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin-top: 15px;
  }

  .form-submit-btn input {
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
    background-color: rgba(181, 71, 55, 0.8);
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

  }

</style>