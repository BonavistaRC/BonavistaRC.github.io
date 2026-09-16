---
layout: default
title: Members
---

## Members
<br>


<html>
<head>
  <meta charset="UTF-8">
  <title>Membership Test</title>
</head>

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
</style>

<body>

<div class="member-update">

  <div id="request-form">
    <h1>Update Your Contact Information</h1>

    <p>
      Enter your membership number to receive a secure link
      to update your contact information.
    </p>

    <form
      id="member-form"
      method="POST"
      action="https://script.google.com/macros/s/AKfycbzBQHMhYB6rTOxEV03TMqMTahRACxwCXSOl86VEbRu3HL8dlHq4YPa8eza4h82S5pcz/exec"
      target="submission-frame"
    >
      <label for="memberNumber">Membership Number</label>

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

      <button type="submit">Continue</button>
    </form>
  </div>


  <div id="confirmation" hidden>
    <h1>Check Your Email</h1>

    <p>
      If the membership number matches our records, we've sent
      an email with a secure link to continue.
	</p>

	<p>
	  The link will expire in 30 minutes.
	</p>

	<p>
	    If you don't receive the email within a few minutes,
	    please check your spam folder.
	</p>

	<p>
	  If you have any issues or need assistance, please contact us at
	  <a href="mailto:info@bonavistarc.com">info@bonavistarc.com</a>.
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
     * of whether the membership number exists.
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

