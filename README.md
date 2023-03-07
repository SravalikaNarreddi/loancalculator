<!DOCTYPE html>
<html>
<head>
	<title>Loan Calculator</title>
</head>
<body>
	<h1>Loan Calculator</h1>
	
	<form>
		<label for="carprice">Car Price:</label>
		<input type="number" id="carprice" name="carprice" required><br><br>
		
		<label for="downpayment">Down Payment:</label>
		<input type="number" id="downpayment" name="downpayment" required><br><br>
		
		<label for="interestrate">Interest Rate:</label>
		<input type="number" id="interestrate" name="interestrate" step="0.01" required><br><br>
		
		<label for="loantenure">Loan Tenure:</label>
		<input type="range" id="loantenure" name="loantenure" min="1" max="10" value="5">
		<span id="loantenurevalue"></span> years<br><br>
		
		<label for="monthlypayment">Monthly Payment:</label>
		<input type="text" id="monthlypayment" name="monthlypayment" readonly><br><br>
	</form>
	
	<script>
		var carprice = document.getElementById("carprice");
		var downpayment = document.getElementById("downpayment");
		var interestrate = document.getElementById("interestrate");
		var loantenure = document.getElementById("loantenure");
		var loantenurevalue = document.getElementById("loantenurevalue");
		var monthlypayment = document.getElementById("monthlypayment");
		
		carprice.addEventListener("input", calculateLoan);
		downpayment.addEventListener("input", calculateLoan);
		interestrate.addEventListener("input", calculateLoan);
		loantenure.addEventListener("input", updateLoanTenure);
		
		function calculateLoan() {
			var loanamount = carprice.value - downpayment.value;
			var months = loantenure.value * 12;
			var interestpermonth = (interestrate.value/100) / 12;
			
			var monthlypaymentvalue = (loanamount * interestpermonth) / (1 - Math.pow(1 + interestpermonth, -months));
			monthlypayment.value = "$" + monthlypaymentvalue.toFixed(2);
		}
		
		function updateLoanTenure() {
			loantenurevalue.innerHTML = loantenure.value;
			calculateLoan();
		}
	</script>
</body>
</html>
