# Enrolment

What is Enrolment?

Say you are a health clinic that provides health care to beneficiaries in your community. You would need a way to keep track of the beneficiary's health records at your clinic, hence you would want to **register** them in your system and store information for subsequent visits, health issues, and treatments.

Registering a new beneficiary is the **enrolment** process in **Simprints ID**.

1. Calling app creates a **Register** Intent using **projectID, moduleID** and **userID** and sends intent to **Simprints ID**
2. Beneficiary's biometrics get captured and processed to generate a **uniqueId** and **biometric template**
3. **Simprints ID** returns the generated **uniqueId** to the calling app
4. Calling app receives the resulting **uniqueId** and stores it with the beneficiary's personal info.

Trigger Enrolment

Simprints ID accepts normal Android intents as requests and you can also use **SimHelper** to streamline creating the intent. To register a new beneficiary, you need to:

// create an instance of **SimHelper**

SimHelper simHelper = new SimHelper("Project ID", "User ID");

// create an **Intent** using the **register** method on the **SimHelper** object

Intent enrolIntent = simHelper.register("Module ID");

// trigger the **Intent** using the [**startActivityForResult**](https://developer.android.com/reference/android/app/Activity#startActivityForResult%28android.content.Intent,%20int%29) method

startActivityForResult(enrolIntent, requestCode); // [r](https://developer.android.com/reference/android/app/Activity#startActivityForResult%28android.content.Intent,%20int%29)[equestCode](https://developer.android.com/reference/android/app/Activity#startActivityForResult%28android.content.Intent,%20int%29) is required for Android intents

Handling Enrolment Response

During the enrolment process, **Simprints ID** captures the beneficiary's biometric data, processes it, and then generates both a biometric **template** and a **unique ID** which are saved in **Simprints ID**, and the **unique ID** is returned to the calling app.

If the enrolment was successful, this **unique ID** is sent back in an **Intent** to the calling Android application.

This **unique ID** should be extracted from the response and saved in your Android application and server together with the beneficiary information. This is how you link a record on your side with a Simprints record.

The response comes via Android as part of the **onActivityResult**:

@Override

public void onActivityResult(int requestCode, int resultCode, Intent data) {

super.onActivityResult(requestCode, resultCode, data)

// check that neither Simprints or Android returned an error

if (resultCode == Activity._RESULT\_OK_) {

// ensure the requestCode is the one you sent for the enrolment request

if (requestCode == enrolRequestCode) {

// call method to handle enrolment

handleEnrolment(data);

}

} else {

// check out [Handling Errors](broken-reference) page for reference

}

}

import com.simprints.libsimprints.Constants;

public void handleEnrolment(Intent data) {

// get the boolean flag to check if biometrics completed successfully

Boolean biometricsCompleted = data.getBooleanExtra(Constants.SIMPRINTS\_BIOMETRICS\_COMPLETE\_CHECK);

if (biometricsCompleted) {

// extract the returned Registration object

Registration registration = data.getParcelableExtra(Constants.SIMPRINTS\_REGISTRATION);

// this is the unique id to be saved with the persons data

String simprintsUniqueId = registration.getGuid();

}

}

Note: the properties of the [**Registration**](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FSimprints%2FLibSimprints%2Fblob%2Fmain%2Fsrc%2Fmain%2Fjava%2Fcom%2Fsimprints%2Flibsimprints%2FRegistration.java\&sa=D\&sntz=1\&usg=AOvVaw3bX6tHm4fvJMoVyfjaAQt-) object are:

* **guid** - a **String** value containing the generated unique identifier (which can be accessed through the **getGuid** method)
* **\[deprecated] template** - a **byte array** containing the generated biometric **template** (which can be accessed through the **getTemplate** method)

Handling Alternate Scenarios

During the enrolment process, the biometric capture and processing might not complete due to two main reasons:

1. A system/application error occurred. To read more on how to handle application errors [check here](broken-reference).
2. The user backed out of completing the process. To read more on how to handle uncompleted workflow issues [check here](broken-reference).

We have a feature called **Enrolment+,** that lets you check if a beneficiary has been enrolled before making a new enrolment. To see how to implement this [check here](broken-reference).
