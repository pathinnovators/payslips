<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<title>Bright Path Innovators Payroll Portal</title>

<style>

*{ box-sizing:border-box; }

body{
font-family:Arial, sans-serif;
background:#f4f6f9;
margin:0;
}

/* HEADER */
.header{
background:#0047AB;
color:white;
text-align:center;
padding:25px 15px;
}

.logo{
width:90px;
height:90px;
border-radius:50%;
object-fit:cover;
margin-bottom:10px;
border:4px solid white;
}

.company{
font-size:24px;
font-weight:bold;
}

.portal{
font-size:15px;
opacity:0.9;
}

/* CARD */
.container{
max-width:420px;
width:92%;
margin:40px auto;
background:white;
padding:25px;
border-radius:10px;
box-shadow:0 0 12px rgba(0,0,0,0.12);
text-align:center;
}

input{
width:100%;
padding:12px;
margin:10px 0;
border:1px solid #ccc;
border-radius:6px;
font-size:15px;
}

button{
width:100%;
padding:12px;
background:#FF2F00;
color:white;
border:none;
border-radius:6px;
font-size:16px;
cursor:pointer;
}

button:hover{
background:#003580;
}

/* CAPTCHA */
.captcha-box{
display:flex;
justify-content:center;
align-items:center;
gap:10px;
margin-top:10px;
}

.captcha{
font-size:20px;
background:#eee;
padding:10px 18px;
letter-spacing:4px;
font-weight:bold;
border-radius:5px;
}

.refresh{
cursor:pointer;
font-size:18px;
}

/* RESULT */
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
<div class="company">Bright Path Innovators Pvt Ltd</div>
<div class="portal">Employee HR Payroll Portal</div>
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

let captchaCode="";

/* CAPTCHA GENERATOR */
function generateCaptcha(){
const chars="ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
captchaCode="";

for(let i=0;i<5;i++){
captchaCode+=chars.charAt(Math.floor(Math.random()*chars.length));
}

document.getElementById("captcha").innerText=captchaCode;
}

generateCaptcha();

/* PAYSLIP DATA (FIXED) */
const payslips=[

{ id:"BPI-006", month:"2025-11", link:"https://drive.google.com/file/d/1xqCvYPTOZWqA27TrcM7BNxZh8EUZkYjh/view" },
{ id:"BPI-011", month:"2025-11", link:"https://drive.google.com/file/d/1AkTESX-ju6g3VDbf5aHXCghxwjwemdzt/view" },

{ id:"BPI-006", month:"2025-12", link:"https://drive.google.com/file/d/1NTBYF2NQi0G7WiqOK8TrU0XJKTKJz51R/view" },
{ id:"BPI-011", month:"2025-12", link:"https://drive.google.com/file/d/1qFB77gRm6D6r9JCz_s06wePbiCQ2jDdT/view" },

{ id:"BPI-006", month:"2026-01", link:"https://drive.google.com/file/d/1qnd22RWqa5TScqstUX1tgTAittIa_Kuz/view" },
{ id:"BPI-011", month:"2026-01", link:"https://drive.google.com/file/d/1tYf3Zn0vO8PlsaiAAOqkkVLp62uGw_BA/view" },

{ id:"BPI-006", month:"2026-02", link:"https://drive.google.com/file/d/1GrKOzxHk8iuH1hg9PitzTT4ojeP5yTlv/view" },
{ id:"BPI-011", month:"2026-02", link:"https://drive.google.com/file/d/13WAqiDIULTc_kDgxRRgFx_Y3lp9-d8w9/view" }

];

/* ACCESS FUNCTION */
function getPayslip(){

let emp=document.getElementById("empID").value.trim();
let month=document.getElementById("month").value;
let captchaInput=document.getElementById("captchaInput").value;
let result=document.getElementById("result");

if(captchaInput!==captchaCode){
alert("Incorrect CAPTCHA");
generateCaptcha();
return;
}

let found=payslips.find(p=>p.id===emp && p.month===month);

if(found){
result.innerHTML=`
<a href="${found.link}" target="_blank">
<button>Download Payslip</button>
</a>
`;
}else{
result.innerHTML="<p style='color:red'>Payslip not found. Please contact HR.</p>";
}

}

</script>

</body>
</html>
