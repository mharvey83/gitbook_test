# Integrating w/ Simprints

This section contains links to information about how to integrate with **Simprints ID**, using a custom Android application. Key features and terminology that **Simprints ID** uses will also be introduced in this section.

What is Simprints ID?

**Simprints ID** is a standalone Android app that is responsible for enrolling and verifying a person's identity, using unique features like the person's fingerprint and face.

The custom app is responsible for capturing any biographical information along with additional data being collected, and **Simprints ID** is responsible for capturing the person's biometric identity. After a new biometric record is created in **Simprints ID,** a unique ID is generated and returned to the custom app. This unique ID is to be stored along with the person's biographical data and any other data collected, within the custom app and servers.

This unique ID, that is stored on the custom app, is what is used to match a newly captured biometric template with a previously enrolled one. When there is the need to verify that a person is who they say they are, a call is made to **Simprints ID** using this unique ID, from which **Simprints ID** will take a new biometric capture with the person present, and validate that it matches the previously enrolled biometric capture with that unique ID.
