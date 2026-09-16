---
layout: default
title: Update Contact Information
---


  <style>

    .member-update {
      max-width: 600px;
      margin: 40px auto;
      padding: 20px;
    }

    .member-update h1 {
      margin-bottom: 20px;
    }

    .member-update p {
      line-height: 1.6;
    }

    .field {
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 6px;
      font-weight: 600;
    }

    input[type="text"],
    input[type="email"],
    input[type="tel"] {
      width: 100%;
      box-sizing: border-box;
      padding: 10px;
      font-size: 16px;
    }

    .radio-option {
      margin: 10px 0;
    }

    .radio-option label {
      display: inline;
      font-weight: normal;
    }

    .preference-note {
      margin: 6px 0 0 25px;
      font-size: 0.95em;
    }

    button {
      padding: 12px 20px;
      font-size: 16px;
      cursor: pointer;
    }

    button:disabled {
      cursor: default;
      opacity: 0.6;
    }

    .button {
      display: inline-block;
      margin-top: 15px;
      padding: 12px 20px;
      text-decoration: none;
      border: 1px solid #555;
      border-radius: 4px;
    }

    .error-message {
      margin: 20px 0;
      font-weight: 600;
    }

    .container {
      max-width: 600px;
      margin: 40px auto;
      padding: 20px;
    }

  </style>


<body>

<main class="member-update">


  <!-- VERIFYING -->

  <div id="verifying" hidden>

    <h1>Verifying Your Link</h1>

    <p>
      Please wait while we verify your secure link.
    </p>

  </div>



  <!-- UPDATE FORM -->

  <div id="verified" hidden>

    <h1>Update Your Contact Information</h1>

    <p>
      Please confirm whether you are still a registered
      owner of the property.
    </p>


    <form id="update-form">

      <input
        type="hidden"
        name="action"
        value="updateMember"
      >

      <input
        type="hidden"
        id="form-token"
        name="token"
      >


      <!-- OWNERSHIP -->

      <div class="field">

        <label>
          Are you currently a registered owner of this property?
        </label>

        <div class="radio-option">

          <input
            type="radio"
            id="owner-current"
            name="ownership"
            value="current"
            required
          >

          <label for="owner-current">
            Yes, I am a registered owner
          </label>

        </div>


        <div class="radio-option">

          <input
            type="radio"
            id="owner-moved"
            name="ownership"
            value="moved"
          >

          <label for="owner-moved">
            No, I am no longer a registered owner
          </label>

        </div>

      </div>



      <!-- CONTACT FIELDS -->

      <div id="contact-fields" hidden>


        <div class="field">

          <label for="phone">
            Phone
          </label>

          <input
            type="tel"
            id="phone"
            name="phone"
            autocomplete="tel"
          >

        </div>


        <div class="field">

          <label for="email">
            Email
          </label>

          <input
            type="email"
            id="email"
            name="email"
            autocomplete="email"
          >

        </div>



        <!-- COMMUNICATION PREFERENCE -->

        <div class="field">

          <label>
            Communication Preference
          </label>


          <div class="radio-option">

            <input
              type="radio"
              id="preference-email"
              name="communicationPreference"
              value="Email"
            >

            <label for="preference-email">
              Email
            </label>

            <p class="preference-note">
              Preferred. Email communication helps us keep
              administrative and mailing costs low.
            </p>

          </div>


          <div class="radio-option">

            <input
              type="radio"
              id="preference-mail"
              name="communicationPreference"
              value="Regular Mail"
            >

            <label for="preference-mail">
              Regular Mail
            </label>

          </div>

        </div>

      </div>



      <!-- MOVED EXPLANATION -->

      <div id="moved-message" hidden>

        <p>
          Thank you for letting us know.
        </p>

        <p>
          We will update our records to indicate that you
          are no longer the registered owner.
        </p>

        <p>
          We will also email you information to provide to
          your realtor or the new property owner.
        </p>

      </div>



      <div
        id="form-error"
        class="error-message"
        hidden
      ></div>

      <button
        id="submit-button"
        type="submit"
        hidden
      >
        Update Contact Information
      </button>


    </form>

  </div>



  <!-- SUCCESS: CURRENT OWNER -->

  <div id="success-current" hidden>

    <h1>Contact Information Updated</h1>

    <p>
      Thank you. Your contact information has been
      successfully updated and your membership record
      has been verified.
    </p>

  </div>



  <!-- SUCCESS: MOVED -->

  <div id="success-moved" hidden>

    <h1>Thank You</h1>

    <p>
      We have updated our records to indicate that you
      are no longer the registered owner.
    </p>

    <p>
      We have emailed you information to provide to your
      realtor or the new property owner.
    </p>

    <p>
      Once the new owner receives their Land Title,
      they should contact
      <a href="mailto:info@bonavistarc.com">
        info@bonavistarc.com
      </a>
      with a copy of the title and their contact information.
    </p>

  </div>



  <!-- EXPIRED -->

  <div id="expired" hidden>

    <h1>Link Expired</h1>

    <p>
      This secure link is invalid or has expired.
    </p>

    <p>
      Please return to the members page and enter your
      membership number to request a new link.
    </p>

    <a
      class="button"
      href="/members/"
    >
      Request a New Link
    </a>

    <p>
      If you have any issues or need assistance,
      please contact us at
      <a href="mailto:info@bonavistarc.com">
        info@bonavistarc.com
      </a>.
    </p>

  </div>



  <!-- NO TOKEN = 404 -->

  <div id="no-token" hidden>

    <div class="container">

      <h1>404</h1>

      <p>
        <strong>Page not found :(</strong>
      </p>

      <p>
        The requested page could not be found.
      </p>

    </div>

  </div>


</main>



<script>

  const APPS_SCRIPT_URL =
    'https://script.google.com/macros/s/AKfycbzBQHMhYB6rTOxEV03TMqMTahRACxwCXSOl86VEbRu3HL8dlHq4YPa8eza4h82S5pcz/exec';


  const params =
    new URLSearchParams(window.location.search);

  const token =
    params.get('token');


  const verifying =
    document.getElementById('verifying');

  const verified =
    document.getElementById('verified');

  const expired =
    document.getElementById('expired');

  const noToken =
    document.getElementById('no-token');

  const contactFields =
    document.getElementById('contact-fields');

  const movedMessage =
    document.getElementById('moved-message');

  const submitButton =
    document.getElementById('submit-button');

  const form =
    document.getElementById('update-form');

  const formError =
    document.getElementById('form-error');


  /*
   * No token = display 404.
   */

  if (!token) {

    noToken.hidden = false;

  } else {

    verifying.hidden = false;

    validateAndLoadMember();

  }



  /*
   * Validate token and then retrieve only the
   * contact information this member may edit.
   */

  async function validateAndLoadMember() {

    try {

      const url =
        APPS_SCRIPT_URL +
        '?action=memberData' +
        '&token=' +
        encodeURIComponent(token);


      const response =
        await fetch(url);


      if (!response.ok) {
        throw new Error(
          'Verification request failed.'
        );
      }


      const result =
        await response.json();


      verifying.hidden = true;


      if (
        !result.success ||
        !result.valid
      ) {

        expired.hidden = false;
        return;

      }


      /*
       * Populate existing information.
       */

      document.getElementById('phone').value =
        result.phone || '';

      document.getElementById('email').value =
        result.email || '';


      if (
        result.communicationPreference === 'Email'
      ) {

        document.getElementById(
          'preference-email'
        ).checked = true;

      } else if (
        result.communicationPreference === 'Regular Mail'
      ) {

        document.getElementById(
          'preference-mail'
        ).checked = true;

      }


      document.getElementById(
        'form-token'
      ).value = token;


      /*
       * Remove the token from the visible browser URL
       * after we've successfully loaded the member.
       *
       * The token remains in the JavaScript variable
       * and hidden form field for submission.
       */

      history.replaceState(
        {},
        document.title,
        window.location.pathname
      );


      verified.hidden = false;


    } catch (error) {

      console.error(error);

      verifying.hidden = true;
      expired.hidden = false;

    }

  }



  /*
   * Current owner selected.
   */

  document
    .getElementById('owner-current')
    .addEventListener('change', function () {

      contactFields.hidden = false;
      movedMessage.hidden = true;

      submitButton.hidden = false;

      submitButton.textContent =
        'Update Contact Information';

      document.getElementById(
        'email'
      ).required = true;

      document.getElementById(
        'preference-email'
      ).required = true;

    });



  /*
   * No longer owner selected.
   */

  document
    .getElementById('owner-moved')
    .addEventListener('change', function () {

      contactFields.hidden = true;
      movedMessage.hidden = false;

      submitButton.hidden = false;

      submitButton.textContent =
        'Notify Us of Ownership Change';

      document.getElementById(
        'email'
      ).required = false;

      document.getElementById(
        'preference-email'
      ).required = false;

    });



  /*
   * Submit update.
   */

  form.addEventListener(
    'submit',
    async function (event) {

      event.preventDefault();

      formError.hidden = true;

      submitButton.disabled = true;
      submitButton.textContent =
        'Updating...';


      try {

        const formData =
  new FormData(form);

const body =
  new URLSearchParams();

for (const [key, value] of formData.entries()) {
  body.append(key, value);
}

const response =
  await fetch(
    APPS_SCRIPT_URL,
    {
      method: 'POST',
      body: body
    }
  );


        if (!response.ok) {
          throw new Error(
            'Update request failed.'
          );
        }


        const result =
          await response.json();


        if (!result.success) {

          if (result.expired) {

            verified.hidden = true;
            expired.hidden = false;

            return;

          }


          throw new Error(
            result.message ||
            'The update could not be completed.'
          );

        }


        /*
         * Successful update.
         */

        verified.hidden = true;


        if (result.moved) {

          document.getElementById(
            'success-moved'
          ).hidden = false;

        } else {

          document.getElementById(
            'success-current'
          ).hidden = false;

        }


      } catch (error) {

        console.error(error);

        formError.textContent =
          error.message ||
          'The update could not be completed. Please try again.';

        formError.hidden = false;

        submitButton.disabled = false;


        const moved =
          document.getElementById(
            'owner-moved'
          ).checked;


        submitButton.textContent =
          moved
            ? 'Notify Us of Ownership Change'
            : 'Update Contact Information';

      }

    }
  );

</script>

