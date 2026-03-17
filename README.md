"<!DOCTYPE html> 
<html lang="en">

<head>

<meta charset="UTF-8">
<title>Bright Path Innovators Payroll Portal</title>

<style>

body{
font-family:Arial, sans-serif;
background:#f4f6f9;
margin:0;
padding:0;
}

.header{
background:#0047AB;
color:white;
text-align:center;
padding:30px;
}

.logo{
width:100px;
height:100px;
border-radius:50%;
object-fit:cover;
margin-bottom:10px;
border:4px solid white;
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
border-radius:12px;
box-shadow:0 0 12px rgba(0,0,0,0.12);
text-align:center;
}

input{
width:95%;
padding:12px;
margin:10px 0;
border:1px solid #ccc;
border-radius:6px;
font-size:15px;
}

input[type="month"]{
background:#fafafa;
cursor:pointer;
}

button{
width:100%;
padding:12px;
background:#FF2F00;
color:white;
border:none;
border-radius:6px;
font-size:20px;
cursor:pointer;
transition:0.3s;
}

button:hover{
background:#003580;
}

.captcha-box{
display:flex;
justify-content:center;
align-items:center;
gap:10px;
margin-top:10px;
}

.captcha{
font-size:22px;
background:#eee;
padding:10px 20px;
letter-spacing:4px;
font-weight:bold;
border-radius:5px;
}

.refresh{
cursor:pointer;
font-size:18px;
}

.result{
margin-top:20px;
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

<input type="month" id="month">

<div class="captcha-box">
<div class="captcha" id="captcha"></div>
<div class="refresh" onclick="generateCaptcha()">🔄</div>
</div>

<input type="text" id="captchaInput" placeholder="Enter CAPTCHA">

<button onclick="getPayslip()">View Payslip</button>

<div class="result" id="result"></div>

</div>

<div class="footer">
© 2026 Bright Path Innovators Pvt Ltd
</div>

<script>

let captchaCode=""

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

const chars="ABCDEFGHJKLMNPQRSTUVWXYZ23456789"
captchaCode=""

for(let i=0;i<5;i++){

captchaCode+=chars.charAt(Math.floor(Math.random()*chars.length))

}

document.getElementById("captcha").innerText=captchaCode

}

generateCaptcha()

function getPayslip(){

let emp=document.getElementById("empID").value.trim()
let month=document.getElementById("month").value
let captchaInput=document.getElementById("captchaInput").value
let result=document.getElementById("result")

if(captchaInput!==captchaCode){

alert("Incorrect CAPTCHA")
generateCaptcha()
return

}

let found=payslips.find(p=>p.id===emp && p.month===month)

if(found){

result.innerHTML=
<a href="${found.link}" target="_blank">
<button>Download Payslip</button>
</a>

}

else{

result.innerHTML="<p style='color:red'>Payslip not found. Please contact HR.</p>"

}

}

</script>

</body>
</html>" rewrite this code to be compatible with both mobile and desktop view
