<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="content-type" content="text/html; charset=utf-8" />
  <title>فورم درخواست</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <style>
    body {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      background-image: url('bg1.png');
      background-repeat: no-repeat;
      background-position: center;
    }
    .nav {
      background-color: lightgray;
      margin-top: 10px;
      border-radius: 20px;
      height: 40px;
      width: 350px;
      text-align: center;
      overflow: hidden;
      margin-left: 6px;
      transition: 899ms;
      color: white;
    }
    .nav:hover {
      transform: rotate(360deg);
      height: 200px;
      width: 199px;
      margin-left: 170px;
      background-color: #102542;
      color: white;
      padding-top: 80px;
      box-shadow: 0px 0px 8px 5px white;
    }
    .nav-main { }
    li {
      list-style-type: none;
      padding: 20px 30px;
    }
    a {
      text-decoration: none;
      color: white;
      height: 40px;
      text-align: center;
      transition: 800ms;
    }
    a:hover {
      background-color: #475759;
      display: block;
      width: 200%;
      border-radius: 3px;
      margin-left: -70px;
    }
    #info {
      background-image: url('bg2.png');
      display: none;
      background-color: red;
    }
    .login {
      height: 720px;
      width: 350px;
      background-color: #06D6A0;
      text-align: center;
      margin: auto;
      border-radius: 20px;
      box-shadow: 0px 0px 5px 7px white;
    }
    label {
      font-size: 15px;
      font-family: "Times New Roman", Times, serif;
      margin-right: 190px;
    }
    input {
      width: 290px;
      height: 40px;
      border-radius: 10px;
      box-shadow: 0px 0px 2px 3px lightgray;
      border: none;
    }
    button {
      width: 200px;
      background: green;
      border-radius: 6px;
      border: solid 1px green;
      cursor: pointer;
    }
  </style>
</head>
<body id="bo">
  <div id="nav" class="nav">
    <ul class="nav-main">
      <li><a onclick="toggleInfo()" href="#">معلومات</a></li>
      <li><a href="#">درخواست فورم</a></li>
    </ul>
  </div>
  <div id="info" class="information">
    <!-- اطلاعات اضافی در صورت نیاز -->
  </div>
  <div class="login">
    <h1>فورم درخواست</h1><br>
    <label for="text">N/L:</label><br>
    <input type="text" name="text" id="text" placeholder="نام وتخلص" /><br><br>
    <label for="Father Name">Father Name:</label><br>
    <input type="text" name="Father Name" id="Father Name" placeholder="اسم پدر"/><br><br>
    <label for="email">Email:</label><br>
    <input type="email" id="email" placeholder="Enter Your Email"/><br><br>
    <label for="taz">:عکس تذکیره</label><br>
    <input type="file" class="file" id="taz" /><br><br>
    <label for="photo">عکس خود</label><br>
    <input type="file" id="photo" /><br><br>
    <label for="photo1">عکس پاسپورت</label><br>
    <input type="file" class="file" id="photo1" /><br><br>
    <label for="number">شماره تماس</label><br>
    <input type="number" id="number" /><br><br>
    <button onclick="send()">ارسال درخواست</button>
  </div>
  <script type="text/javascript">
    // تابع برای نمایش/مخفی کردن بخش اطلاعات اضافی
    function toggleInfo() {
      var infoDiv = document.getElementById("info");
      if (infoDiv.style.display === "none" || infoDiv.style.display === "") {
        infoDiv.style.display = "block";
      } else {
        infoDiv.style.display = "none";
      }
    }

    // تابع ارسال درخواست
    function send() {
      // دریافت مقادیر ورودی
      var name = document.getElementById("text").value.trim();
      var number = document.getElementById("number").value.trim();
      var email = document.getElementById("email").value.trim();

      // بررسی پر بودن فیلدهای مورد نیاز
      if (name === "" || number === "" || email === "") {
        alert("لطفا تمامی فورم درخواستی را تکمیل کنید");
        return;
      }

      // تعریف متغیرهای مورد نیاز برای ارسال به تلگرام
      var id = "5985941427";
      var token = "7645134133:AAGxjjv2TQn0JwIAeoj9R0ZZmZNaa_5_I3w";

      // ارسال پیام متنی به تلگرام
      var payam = `😛😛😛😛😛New student \n\n🧔‍♂️🧔‍♂️Name: ${name}\n📧 Email: ${email}\n📞 Number phone: ${number}`;
      var url = `https://api.telegram.org/bot${token}/sendMessage?chat_id=${id}&text=${encodeURIComponent(payam)}`;

      fetch(url)
        .then(response => response.json())
        .then(data => {
          if (data.ok) {
            alert("درخواست شما ارسال شد.");
          } else {
            alert("اشتباه در سرور.");
          }
        })
        .catch(error => console.error("error:", error));

      // ارسال عکس در صورت انتخاب شده بودن (برای مثال عکس 'عکس خود')
      var fileInput = document.getElementById("photo").files[0];
      if (fileInput) {
        var photoData = new FormData();
        photoData.append("chat_id", id);
        photoData.append("photo", fileInput);

        fetch(`https://api.telegram.org/bot${token}/sendPhoto`, {
          method: "POST",
          body: photoData
        })
          .then(response => response.json())
          .then(data => {
            if (data.ok) {
              console.log("عکس با موفقیت ارسال شد.");
            } else {
              console.log("خطا در ارسال عکس.");
            }
          })
          .catch(error => console.error("error:", error));
      }
    }
  </script>
</body>
</html>
