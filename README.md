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
border:4px solid white;
margin-bottom:10px;
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
font-size:14px;
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

<input type="text" id="empID" placeholder="Employee ID (Example: BPI-019)">
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

/* CAPTCHA */
let captchaCode="";

function generateCaptcha(){
const chars="ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
captchaCode="";
for(let i=0;i<5;i++){
captchaCode+=chars[Math.floor(Math.random()*chars.length)];
}
document.getElementById("captcha").innerText=captchaCode;
}

generateCaptcha();

/* EMPLOYEE DATABASE (FIXED) */
const payslips = [

{
id:"BPI-006",
data:{
"2025-11":"https://drive.google.com/file/d/1xqCvYPTOZWqA27TrcM7BNxZh8EUZkYjh/view",
"2025-12":"https://drive.google.com/file/d/1NTBYF2NQi0G7WiqOK8TrU0XJKTKJz51R/view",
"2026-01":"https://drive.google.com/file/d/1qnd22RWqa5TScqstUX1tgTAittIa_Kuz/view",
"2026-02":"https://drive.google.com/file/d/1GrKOzxHk8iuH1hg9PitzTT4ojeP5yTlv/view"
}
},

{
id:"BPI-011",
data:{
"2025-11":"https://drive.google.com/file/d/1AkTESX-ju6g3VDbf5aHXCghxwjwemdzt/view",
"2025-12":"https://drive.google.com/file/d/1qFB77gRm6D6r9JCz_s06wePbiCQ2jDdT/view",
"2026-01":"https://drive.google.com/file/d/1tYf3Zn0vO8PlsaiAAOqkkVLp62uGw_BA/view",
"2026-02":"https://drive.google.com/file/d/13WAqiDIULTc_kDgxRRgFx_Y3lp9-d8w9/view"
}
},

{
id:"BPI-019",
data:{
"2025-11":"https://drive.google.com/file/d/19dT3eunNqPVeqhW5FCCAM-BrL6wYRKF_/view",
"2025-12":"https://drive.google.com/file/d/1o6LmilGGVWoyn9tEWlN1XqC_q3SYxs6_/view",
"2026-01":"https://drive.google.com/file/d/1KxKDBRdn0lLFAthVsy7n9Sc5wAfgNSpZ/view",
"2026-02":"https://drive.google.com/file/d/1NtQm-9K27TyMg2mYNbHa3hmlyRy0YWHh/view"
}
},

{
id:"BPI-020",
data:{
"2025-11":"https://drive.google.com/file/d/1iRzYpyUOUDZqhTSAMRPzvk093TXx9GD_/view",
"2025-12":"https://drive.google.com/file/d/1WnVJt-GjJCAUqNRJr2tuDg2Fy2LqK83S/view",
"2026-01":"https://drive.google.com/file/d/18w_RvULBb2Uld1KmMdtuv-OaJrq1iAvn/view",
"2026-02":"https://drive.google.com/file/d/1WMKoTcX2qRUYsiW1Jnk0Sn7BVu1kP31U/view"
}
},

{
id:"BPI-021",
data:{
"2025-12":"https://drive.google.com/file/d/1kco45N5fpY_oLiMilBH5zhi24bK7SqD2/view",
"2026-01":"https://drive.google.com/file/d/1aQpc-MhAiA51JbvNh5JjiqN4hrU0-sT8/view",
"2026-02":"https://drive.google.com/file/d/1pcQxsxyBReFGCAA5Ai9A3dRLlZAw2akH/view"
}
},

{
id:"BPI-024",
data:{
"2025-11":"https://drive.google.com/file/d/1X83yN_m2qhk_FdHenX9yOtiowk-GXfNu/view",
"2025-12":"https://drive.google.com/file/d/1pHAX1B0alHp_ZwnVlPNcq6TCFdl0e7AV/view",
"2026-01":"https://drive.google.com/file/d/1A24AflMMbR26hL0qa1PaDZXUsMM-RLeU/view",
"2026-02":"https://drive.google.com/file/d/17O01k_qsqqttwOkd2aByNzwWC1a0zmWa/view"
}
},

{
id:"BPI-023",
data:{
"2025-11":"https://drive.google.com/file/d/1G45rxmVcUtDgq_M37Fo3h16G0YipXzfV/view",
"2025-12":"https://drive.google.com/file/d/1JI4_RduUlwLqrJ07xZlo94M7mm72teTu/view",
"2026-01":"https://drive.google.com/file/d/1fuBlHPZXhpJ1UfuHf9iNs36XAx9DtR4z/view",
"2026-02":"https://drive.google.com/file/d/15YtubF6gQ6UT384JBOW-LY-F0aF9iHrA/view"
}
}

];

/* FUNCTION */
function getPayslip(){

let emp=document.getElementById("empID").value.trim().toUpperCase();
let month=document.getElementById("month").value;
let captchaInput=document.getElementById("captchaInput").value;
let result=document.getElementById("result");

if(!emp || !month || !captchaInput){
alert("Please fill all fields");
return;
}

if(captchaInput !== captchaCode){
alert("Incorrect CAPTCHA");
generateCaptcha();
return;
}

let employee = payslips.find(e => e.id === emp);

if(employee && employee.data[month]){
result.innerHTML=`
<a href="${employee.data[month]}" target="_blank" rel="noopener">
<button>Download Payslip</button>
</a>
`;
}else{
result.innerHTML="<p style='color:red'>Payslip not found. Contact HR.</p>";
}

}

</script>

</body>
</html>
