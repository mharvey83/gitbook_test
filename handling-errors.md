# Handling Errors

How to Handle Errors

When a biometric flow fails, it can be due to a number of reasons outside an [exit form](broken-reference). Those errors appear for the user in the form of coloured screens. So when handling the result from a flow and an error occurs, you can get access to what type of error occurred using the **Constants** class.

Extracting the error:

import com.simprints.libsimprints.Constants;

override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {

super.onActivityResult(requestCode, resultCode, data)

// ensure that the result status is OK

if (resultCode != Activity._RESULT\_OK_) {

//...code to extract the error that occurred

// using the Constants class

// for instance, an error due to invalid project id

boolean isProjectIdError = resultCode == Constants.SIMPRINTS\_INVALID\_PROJECT\_ID

} else {

//...code to handle success case

}

}
