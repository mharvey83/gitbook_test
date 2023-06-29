# Exit Forms

@Override

protected void onActivityResult(int requestCode, int resultCode, Intent data) {

if (resultCode != Activity.RESULT\_OK) {

//... code to handle error

} else {

//... code to check requestCode and resultCode

// extract the boolean flag to indicating if the flow completed

Boolean biometricsCompleted = data.getBooleanExtra(Constants.SIMPRINTS\_BIOMETRICS\_COMPLETE\_CHECK);

// check if the flow completed successfully

if (biometricsCompleted) {

//...code to handle success scenario

} else {

// check if this was actually due to an exit form

if (data.hasExtra(Constants.SIMPRINTS\_REFUSAL\_FORM)) {

// extract the RefusalForm value

RefusalForm refusalForm = data.getParcelableExtra(Constants.SIMPRINTS\_REFUSAL\_FORM);

// get access to the 'reason' and 'extra' values

String reason = refusalForm.getReason();

tring extra = refusalForm.getExtra();

} else {

//... code to handle alternate error scenario

}

}

}

}
