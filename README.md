<!DOCTYPE html>
<html lang="en">

<head>

<meta charset="UTF-8">
<title>Bright Path Innovators Payroll Portal</title>

<script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>

<style>

body{
font-family:Arial;
background:#f4f6f9;
margin:0;
padding:0;
}

.header{
background:#1e2a38;
color:white;
text-align:center;
padding:25px;
}

.logo{
width:90px;
margin-bottom:10px;
}

.company{
font-size:26px;
font-weight:bold;
}

.portal{
font-size:16px;
opacity:0.9;
}

.container{
width:420px;
margin:60px auto;
background:white;
padding:30px;
border-radius:10px;
box-shadow:0 0 10px rgba(0,0,0,0.1);
text-align:center;
}

input{
width:95%;
padding:12px;
margin:10px 0;
border:1px solid #ccc;
border-radius:6px;
}

button{
width:100%;
padding:12px;
background:#2c3e50;
color:white;
border:none;
border-radius:6px;
font-size:16px;
cursor:pointer;
}

button:hover{
background:#34495e;
}

.result{
margin-top:20px;
}

.captcha{
font-size:22px;
background:#eee;
padding:10px;
letter-spacing:4px;
margin-top:10px;
}

.footer{
text-align:center;
margin-top:40px;
color:#777;
font-size:13px;
}

</style>

</head>

<body>

<div class="header">

<img src="logo.png" class="logo">

<div class="company">
Bright Path Innovators Pvt Ltd
</div>

<div class="portal">
Employee HR Payroll Portal
</div>

</div>

<div class="container">

<h3>Access Your Payslip</h3>

<input type="text" id="empID" placeholder="Employee ID (Example: BPI-021)">

<input type="email" id="email" placeholder="Enter Your Email">

<input type="month" id="month">

<div class="captcha" id="captcha"></div>

<input type="text" id="captchaInput" placeholder="Enter CAPTCHA">

<button onclick="sendOTP()">Send OTP</button>

<input type="text" id="otpInput" placeholder="Enter OTP">

<button onclick="verifyOTP()">Verify & View Payslip</button>

<div class="result" id="result"></div>

</div>

<div class="footer">
© 2026 Bright Path Innovators Pvt Ltd
</div>

<script>

emailjs.init("zzWOW2lsY5ChRSORm")

let captchaCode
let generatedOTP

const payslips=[

<!-- NOVEMBER 2025 -->

{
id:"BPI-006",
month:"2025-11",
link:"https://drive.google.com/file/d/1xqCvYPTOZWqA27TrcM7BNxZh8EUZkYjh/view?usp=sharing"
},

{
id:"BPI-011",
month:"2025-11",
link:"https://drive.google.com/file/d/1AkTESX-ju6g3VDbf5aHXCghxwjwemdzt/view?usp=sharing"
},

{
id:"BPI-019",
month:"2025-11",
link:"https://drive.google.com/file/d/19dT3eunNqPVeqhW5FCCAM-BrL6wYRKF_/view?usp=sharing"
},

{
id:"BPI-020",
month:"2025-11",
link:"https://drive.google.com/file/d/1iRzYpyUOUDZqhTSAMRPzvk093TXx9GD_/view?usp=sharing"
},

{
id:"BPI-024",
month:"2025-11",
link:"https://drive.google.com/file/d/1X83yN_m2qhk_FdHenX9yOtiowk-GXfNu/view?usp=sharing"
},

{
id:"BPI-023",
month:"2025-11",
link:"https://drive.google.com/file/d/1G45rxmVcUtDgq_M37Fo3h16G0YipXzfV/view?usp=sharing"
}

<!-- DECEMBER 2025 -->

{
id:"BPI-006",
month:"2025-12",
link:"https://drive.google.com/file/d/1NTBYF2NQi0G7WiqOK8TrU0XJKTKJz51R/view?usp=sharing"
},

{
id:"BPI-011",
month:"2025-12",
link:"https://drive.google.com/file/d/1qFB77gRm6D6r9JCz_s06wePbiCQ2jDdT/view?usp=sharing"
},

{
id:"BPI-019",
month:"2025-12",
link:"https://drive.google.com/file/d/1o6LmilGGVWoyn9tEWlN1XqC_q3SYxs6_/view?usp=sharing"
},

{
id:"BPI-021",
month:"2025-12",
link:"https://drive.google.com/file/d/1kco45N5fpY_oLiMilBH5zhi24bK7SqD2/view?usp=sharing"
}


{
id:"BPI-020",
month:"2025-12",
link:"https://drive.google.com/file/d/1WnVJt-GjJCAUqNRJr2tuDg2Fy2LqK83S/view?usp=sharing"
},

{
id:"BPI-024",
month:"2025-12",
link:"https://drive.google.com/file/d/1pHAX1B0alHp_ZwnVlPNcq6TCFdl0e7AV/view?usp=sharing"
},

{
id:"BPI-023",
month:"2025-12",
link:"https://drive.google.com/file/d/1JI4_RduUlwLqrJ07xZlo94M7mm72teTu/view?usp=sharing"
}

<!-- JANUARY 2026 -->

{
id:"BPI-006",
month:"2026-01",
link:"https://drive.google.com/file/d/1qnd22RWqa5TScqstUX1tgTAittIa_Kuz/view?usp=sharing"
},

{
id:"BPI-011",
month:"2026-01",
link:"https://drive.google.com/file/d/1tYf3Zn0vO8PlsaiAAOqkkVLp62uGw_BA/view?usp=sharing"
},

{
id:"BPI-019",
month:"2026-01",
link:"https://drive.google.com/file/d/1KxKDBRdn0lLFAthVsy7n9Sc5wAfgNSpZ/view?usp=sharing"
},

{
id:"BPI-021",
month:"2026-01",
link:"https://drive.google.com/file/d/1aQpc-MhAiA51JbvNh5JjiqN4hrU0-sT8/view?usp=sharing"
}


{
id:"BPI-020",
month:"2026-01",
link:"https://drive.google.com/file/d/18w_RvULBb2Uld1KmMdtuv-OaJrq1iAvn/view?usp=sharing"
},

{
id:"BPI-024",
month:"2026-01",
link:"https://drive.google.com/file/d/1A24AflMMbR26hL0qa1PaDZXUsMM-RLeU/view?usp=sharing"
},

{
id:"BPI-023",
month:"2026-01",
link:"https://drive.google.com/file/d/1fuBlHPZXhpJ1UfuHf9iNs36XAx9DtR4z/view?usp=sharing"
}

<!-- FEBRUARY 2026 -->

{
id:"BPI-006",
month:"2026-01",
link:"https://drive.google.com/file/d/1GrKOzxHk8iuH1hg9PitzTT4ojeP5yTlv/view?usp=sharing"
},

{
id:"BPI-011",
month:"2026-01",
link:"https://drive.google.com/file/d/13WAqiDIULTc_kDgxRRgFx_Y3lp9-d8w9/view?usp=sharing"
},

{
id:"BPI-019",
month:"2026-01",
link:"https://drive.google.com/file/d/1NtQm-9K27TyMg2mYNbHa3hmlyRy0YWHh/view?usp=sharing"
},

{
id:"BPI-021",
month:"2026-01",
link:"https://drive.google.com/file/d/1pcQxsxyBReFGCAA5Ai9A3dRLlZAw2akH/view?usp=sharing"
}


{
id:"BPI-020",
month:"2026-01",
link:"https://drive.google.com/file/d/1WMKoTcX2qRUYsiW1Jnk0Sn7BVu1kP31U/view?usp=sharing"
},

{
id:"BPI-024",
month:"2026-01",
link:"https://drive.google.com/file/d/17O01k_qsqqttwOkd2aByNzwWC1a0zmWa/view?usp=sharing"
},

{
id:"BPI-023",
month:"2026-01",
link:"https://drive.google.com/file/d/15YtubF6gQ6UT384JBOW-LY-F0aF9iHrA/view?usp=sharing"
}

<!-- MARCH 2026 -->


]

function generateCaptcha(){

captchaCode=Math.floor(1000+Math.random()*9000)

document.getElementById("captcha").innerText=captchaCode

}

generateCaptcha()

function sendOTP(){

let captchaInput=document.getElementById("captchaInput").value
let email=document.getElementById("email").value
let empid=document.getElementById("empID").value

if(captchaInput != captchaCode){

alert("Incorrect CAPTCHA")
generateCaptcha()
return

}

generatedOTP=Math.floor(100000+Math.random()*900000)

let params={
empid:empid,
otp:generatedOTP,
to_email:email
}

emailjs.send("service_0aucna2","template_e3awo5b",params)

.then(function(){

alert("OTP Sent to your Email")

})

}

function verifyOTP(){

let enteredOTP=document.getElementById("otpInput").value
let emp=document.getElementById("empID").value.trim()
let month=document.getElementById("month").value
let result=document.getElementById("result")

if(enteredOTP != generatedOTP){

alert("Invalid OTP")
return

}

let found=payslips.find(p=>p.id===emp && p.month===month)

if(found){

result.innerHTML=
`<a href="${found.link}" target="_blank">
<button>Download Payslip</button>
</a>`

}

else{

result.innerHTML="<p style='color:red'>Payslip not found. Contact HR.</p>"

}

}

</script>

</body>
</html>
