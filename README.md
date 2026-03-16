<!DOCTYPE html>
<html lang="en">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<title>Bright Path Innovators Payroll Portal</title>

<style>

*{
box-sizing:border-box;
}

body{
font-family:Arial, sans-serif;
background:#f4f6f9;
margin:0;
padding:0;
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

/* MAIN CONTAINER */

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

.container h3{
margin-bottom:15px;
}

/* INPUTS */

input{
width:100%;
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

/* BUTTON */

button{
width:100%;
padding:12px;
background:#FF2F00;
color:white;
border:none;
border-radius:6px;
font-size:18px;
cursor:pointer;
transition:0.3s;
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
flex-wrap:wrap;
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
font-size:20px;
}

/* RESULT */

.result{
margin-top:20px;
}

/* FOOTER */

.footer{
text-align:center;
margin-top:40px;
color:#777;
font-size:13px;
padding-bottom:20px;
}

/* MOBILE OPTIMIZATION */

@media(max-width:480px){

.logo{
width:70px;
height:70px;
}

.company{
font-size:20px;
}

.portal{
font-size:14px;
}

.container{
padding:20px;
}

button{
font-size:16px;
}

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

{
id:"BPI-006",
month:"2025-12",
link:"https://drive.google.com/file/d/1qnd22RWqa5TScqstUX1tgTAittIa_Kuz/view?usp=sharing"
},

{
id:"BPI-011",
month:"2025-12",
link:"https://drive.google.com/file/d/1tYf3Zn0vO8PlsaiAAOqkkVLp62uGw_BA/view?usp=sharing"
},

{
id:"BPI-019",
month:"2025-12",
link:"https://drive.google.com/file/d/1KxKDBRdn0lLFAthVsy7n9Sc5wAfgNSpZ/view?usp=sharing"
},

{
id:"BPI-021",
month:"2025-12",
link:"https://drive.google.com/file/d/1aQpc-MhAiA51JbvNh5JjiqN4hrU0-sT8/view?usp=sharing"
},

{
id:"BPI-020",
month:"2025-12",
link:"https://drive.google.com/file/d/18w_RvULBb2Uld1KmMdtuv-OaJrq1iAvn/view?usp=sharing"
},

{
id:"BPI-024",
month:"2025-12",
link:"https://drive.google.com/file/d/1A24AflMMbR26hL0qa1PaDZXUsMM-RLeU/view?usp=sharing"
},

{
id:"BPI-023",
month:"2025-12",
link:"https://drive.google.com/file/d/1fuBlHPZXhpJ1UfuHf9iNs36XAx9DtR4z/view?usp=sharing"
}

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

result.innerHTML=`
<a href="${found.link}" target="_blank">
<button>Download Payslip</button>
</a>
`

}

else{

result.innerHTML="<p style='color:red'>Payslip not found. Please contact HR.</p>"

}

}

</script>

</body>
</html>
