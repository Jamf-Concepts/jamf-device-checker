# FAQ

## General

**Is Jamf Device Checker free?**
Yes. Jamf Device Checker is a free app available through the Apple App Store and Apple Business Manager / Apple School Manager.

**Who makes Jamf Device Checker?**
Jamf Device Checker is built and maintained by [Jamf](https://www.jamf.com) as part of the Jamf Concepts program.

**Does this app require a Jamf Pro license?**
Yes. Jamf Device Checker is designed for devices managed by Jamf Pro (version 11.25 or later). The app is configured entirely through Jamf Pro's Managed App Config and will not function on unmanaged devices.

---

## Compatibility

**What platforms does Jamf Device Checker support?**
iOS and iPadOS 18.6 or later. macOS and visionOS are not supported.

**Does it work with third-party MDM solutions?**
Jamf Device Checker is designed for Jamf Pro. It relies on the Jamf Pro API for OS-level status information and on Jamf-specific Managed App Config keys, so third-party MDMs are not supported.

**Does the device need to be supervised?**
The device must be enrolled in Jamf Pro. Supervision is not required for the readiness dashboard itself, though standard Jamf Pro management requirements apply.

---

## Setup & Configuration

**Do end users need to sign in or configure anything?**
No. The app configures itself automatically from Managed App Config when deployed through Jamf Pro. End users just open the app.

**Where do I get the sample Managed App Config?**
See the [Managed Configuration](Getting-Started#managed-configuration) section of the Getting Started guide, or the `DeviceCheckerAppConfigSample` file in the source repository.

**Which Jamf Pro API privileges are required?**
The OAuth API client used by the app needs: *Send Device Information Command*, *View MDM command information in Jamf Pro API*, *Read Mobile Devices*, and *Send MDM command information in Jamf Pro API*.

---

## Troubleshooting

**The app shows "Not managed" or won't load status.**
Confirm the device is enrolled in Jamf Pro and that the app has an active Managed App Config payload scoped to it. The required `JPS_URL`, `JSSID`, `MANAGEMENTID`, and `OAUTH_AUTH_CODE` keys must all be populated by Jamf Pro variables.

**A status tile isn't appearing.**
Each tile is controlled by an enable/disable key in Managed App Config (e.g. `device-checker-storage-enabled`). Check that the corresponding key is set to `YES`.

**The OS version tile is red but my device is up to date.**
Check the `device-checker-os-min-version` value in your Managed App Config — the tile compares against that minimum, not the latest available iOS version.

---

## Privacy & Data

**What data does Jamf Device Checker collect?**
The app reads device status locally (OS version, battery, storage, network, etc.) and communicates with your organization's Jamf Pro server via authenticated API calls. It does not send data to Jamf or any third party.

**Does the app require internet access?**
Yes. The app needs connectivity to reach your Jamf Pro server for OAuth token refresh and status updates. Cached status is shown when the server is temporarily unreachable.

---

*Have a question not answered here? [Open a GitHub issue](../../issues/new?template=general_question.yml).*
