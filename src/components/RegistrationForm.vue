<template>
  <div class="container">
    <h1 class="form-title">在這裡註冊</h1>
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
        <textarea name="otherPets" id="otherPets" rows="3"placeholder="你養了甚麼特別的寵物?"></textarea>
      </div>

      <div class="form-submit-btn">
        <input type="submit" value="送出">
        <input type="reset" value="重填">
      </div>
    </form>
  </div>
</template>