---
layout: default
title: Members
---


<html>

<style>
.member-update {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
}

.member-update label {
  display: block;
  font-weight: 600;
  margin: 25px 0 8px;
}

.member-update input {
  box-sizing: border-box;
  width: 100%;
  padding: 12px;
  font-size: 18px;
  border: 1px solid #aaa;
  border-radius: 4px;
}

.member-update button {
  margin-top: 20px;
  padding: 12px 24px;
  font-size: 16px;
  cursor: pointer;
}

.member-update button:disabled {
  cursor: wait;
  opacity: 0.7;
}

#confirmation {
  text-align: center;
  max-width: 550px;
  margin: 0 auto;
}

/* Button */
.button {
  background-color: #4fcdcf; /* Pastel Green */
  color: #fff;
  padding: 17px;
  text-align: center;
  text-decoration: none;
  text-decoration-color: #fff;
  display: inline-block;
  border-radius: 2px;
  border: none;
}

.button:hover {
  opacity: .8 ;
  color: white;
  text-decoration: none;
}

/* Links */

</style>

<body>

<div class="member-update">

  <div id="request-form">
    <h1>Member Portal</h1>
    <p>
      Enter your Member Number and we'll email a secure link to the address on file.
    </p>
    <p>Don't know your Member Number? Contact us at
      <a href="mailto:info@bonavistarc.com">info@bonavistarc.com</a>
    </p>

    <form
      id="member-form"
      method="POST"
      action="https://script.google.com/macros/s/AKfycbzBQHMhYB6rTOxEV03TMqMTahRACxwCXSOl86VEbRu3HL8dlHq4YPa8eza4h82S5pcz/exec"
      target="submission-frame"
    >
      <label for="memberNumber">Member Number</label>

      <input
        type="text"
        id="memberNumber"
        name="memberNumber"
        autocomplete="off"
        required
      >
      <input
        type="hidden"
        name="action"
        value="requestVerification"
      >

      <button class="button" type="submit">Continue</button>
    </form>
  </div>


  <div id="confirmation" hidden>
    <h1>Check Your Email</h1>

    <p>
      If your Member Number matchs our records, you'll receive a secure link shortly. Please check your spam folder if it doesn't arrive.
	</p>



	<p>
	  Need help? Contact us at
	  <a href="mailto:info@bonavistarc.com">info@bonavistarc.com</a>
	</p>
  </div>


  <iframe
    name="submission-frame"
    id="submission-frame"
    style="display:none;">
  </iframe>

</div>


<script>
document
  .getElementById('member-form')
  .addEventListener('submit', function () {

    // Disable the button so it can't be repeatedly clicked.
    const button = this.querySelector('button');

    button.disabled = true;
    button.textContent = 'Sending...';

    /*
     * We intentionally show the same confirmation regardless
     * of whether the member number exists.
     *
     * The Apps Script will perform the actual lookup.
     */
    setTimeout(function () {

      document.getElementById('request-form').hidden = true;
      document.getElementById('confirmation').hidden = false;

    }, 750);

  });
</script>


</body>
</html>

