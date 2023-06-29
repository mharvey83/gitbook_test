# Verification

What is Verification?

Still continuing with the clinic scenario, if you have a beneficiary come to your clinic with their clinic card, you will need to verify that the beneficiary is who they say they are.

This **verification** process involves matching previously enrolled biometric data with the present beneficiary's biometric.

1. Calling app creates a **Verify** Intent using **projectID, moduleID, userID,** and beneficiary's **uniqueID** and sends intent to **Simprints ID**
2. Beneficiary's biometrics gets captured and processed to validate that it matches with previously enrolled biometrics using provided **uniqueID**
3. **Simprints ID** returns the verification result to calling app
4. Calling app receives verification results, and handles the success or failure workflow.

Trigger Verification

To trigger a **verification** process, you need to do the following:

// get the **unique ID** from the existing beneficiary's record

String verifyGuid;

// create an instance of **SimHelper**

SimHelper simHelper = SimHelper("PROJECT ID", "USER ID");

// create an **Intent** using the **verify** method on the **SimHelper** object using the **unique ID**

Intent verificationIntent = simHelper.verify("MODULE ID", verifyGuid);

// trigger the **Intent** using the [**startActivityForResult**](https://developer.android.com/reference/android/app/Activity#startActivityForResult%28android.content.Intent,%20int%29) method

startActivityForResult(verificationIntent, requestCode); // [r](https://developer.android.com/reference/android/app/Activity#startActivityForResult%28android.content.Intent,%20int%29)[equestCode](https://developer.android.com/reference/android/app/Activity#startActivityForResult%28android.content.Intent,%20int%29) is required for Android intents

Handling Verification Response

During the verification process, the present beneficiary's biometrics are captured, and the **verifyGuid** which is passed in the **Intent** is used to retrieve the previously enroled beneficiary's biometrics. The two biometric records are then compared.

If this **verification** process completes successfully, a verification result containing the following properties is returned:

* **Tier** - the ranking tier for the biometric record
* **Confidence** - the percentage to which the record **matches** the captured biometric
* **Guid -** the unique id for the biometric record

Note: The **confidence** and **tier** values can then be used to determine the ranking and accuracy for the matched biometric record, to get more info on this, [check here](broken-reference).

public void onActivityResult(int requestCode, int resultCode, Intent data) {

super.onActivityResult(requestCode, resultCode, data)

// ensure the resultCode is okay

if (resultCode == Activity._RESULT\_OK_) {

// ensure the requestCode is for verification

if (requestCode == verifyRequestCode) {

// handle the verification result

handleVerification(data);

}

} else {

// check out [Handling Errors](broken-reference) page for reference

}

}

import com.simprints.libsimprints.Constants;

private void handleVerification(Intent data) {

// get the boolean flag to check if biometrics completed successfully

Boolean biometricsCompleted = data.getBooleanExtra(Constants.SIMPRINTS\_BIOMETRICS\_COMPLETE\_CHECK);

if (biometricsCompleted) {

// extract the returned Verification object

Verification verification = data.getParcelableExtra(Constants._SIMPRINTS\_VERIFICATION_);

// get tier and confidence score

Tier tier = verification.getT_ier_()

float confidence = verification.getC_onfidence();_

}

}

Handling Alternate Scenarios

During the enrolment process, the biometric capture and processing might not complete due to two main reasons:

1. A system/application error occurred. To read more on how to handle application errors [check here](broken-reference).
2. The user backed out of completing the process. To read more on how to handle uncompleted workflow issues [check here](broken-reference).
