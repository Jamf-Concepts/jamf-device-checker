# Getting Started

## Prerequisites

Before you begin, make sure you have:

- [ ] A Jamf Pro instance (version 11.25 or later) with admin access
- [ ] An Apple Business Manager or Apple School Manager account linked to Jamf Pro (for volume-purchase deployment)
- [ ] Target devices enrolled in Jamf Pro and running iOS/iPadOS 18.6 or later
- [ ] A Jamf Pro API role and Client with the required privileges (see [Managed Configuration](#managed-configuration) below)

## Installation

### Via Apple Business Manager / Volume Purchase (Recommended)

1. Find **Jamf Device Checker** in [Apple Business Manager](https://business.apple.com) or [Apple School Manager](https://school.apple.com).
2. Purchase (free) and assign licenses to the location linked to your Jamf Pro instance.
3. In Jamf Pro, sync your VPP/location token and add **Jamf Device Checker** as a Mobile Device App.
4. Scope the app to your target smart or static device group and set it to install automatically.
5. Configure the Managed App Config payload (see below) so the app is fully set up on first launch.

### Direct Download (Personal Devices)

1. Open the **App Store** on your device.
2. Search for **Jamf Device Checker** or [tap this link](https://apps.apple.com/app/id6761016825).
3. Tap **Get** to install.

> **Note:** Direct-download installs still require the device to be enrolled in a Jamf Pro instance that pushes Managed App Config — the app is designed for managed devices.

## First-Run Setup

Jamf Device Checker automatically configures itself from Managed App Config when deployed via Jamf Pro — end users do not need to sign in or configure anything.

For admins deploying for the first time:

1. Push the app to a test device with a Managed App Config payload populated (see [Managed Configuration](#managed-configuration)).
2. Launch the app on the test device. It should read the payload, complete OAuth setup silently, and display the readiness dashboard.
3. Confirm each enabled tile shows the expected status. Adjust thresholds and enabled checks in your config as needed.
4. Once verified, scope the deployment to your broader device population.

## Managed Configuration

Jamf Device Checker is configured entirely through MDM Managed App Config. Below is a reference of the keys you can set. Values are provided as strings.

### Required (auto-populated by Jamf Pro)

These keys are populated by Jamf Pro variables — do not modify:

| Key | Description |
|---|---|
| `JPS_URL` | Jamf Pro server URL (`$JPS_URL`) |
| `JSSID` | Device Jamf record ID (`$JSSID`) |
| `MANAGEMENTID` | Management ID (`$MANAGEMENTID`) |
| `OAUTH_AUTH_CODE` | OAuth authorization code (`$OAUTH_AUTH_CODE`) |
| `APP_CONFIG_REINSTALL_CODE` | App config reinstall code (`$APP_CONFIG_REINSTALL_CODE`) |
| `APPJSSID` | App JSS ID (`$APPJSSID`) |

### Branding & UI

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-branding-image-url` | String (URL) | Company logo displayed at the top of the app | `` (none) |
| `device-checker-branding-image-height` | String (Int) | Logo height in points | `80` |
| `device-checker-status-tab-scrollable` | String (YES/NO) | When `YES`, the entire Status tab scrolls; otherwise only tiles scroll | `NO` |

### OS & App Readiness

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-os-enabled` | String (YES/NO) | Enable OS version check | `YES` |
| `device-checker-os-min-version` | String | Minimum required iOS version (e.g. `18.0`) | — |
| `device-checker-os-deadline` | String (YYYY-MM-DD) | Deadline to reach the minimum version | — |
| `device-checker-apps-enabled` | String (YES/NO) | Enable required-apps check | `NO` |
| `device-checker-apps-list` | String | Pipe-delimited list: `Name,bundleID,version,deadline` per app | — |

### Status Tiles

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-power-source-enabled` | String (YES/NO) | Show battery-percentage tile | `YES` |
| `device-checker-power-source-warning` | String (Int) | Warning threshold (%) | `25` |
| `device-checker-power-source-critical` | String (Int) | Critical threshold (%) | `10` |
| `device-checker-storage-enabled` | String (YES/NO) | Show storage tile | `YES` |
| `device-checker-storage-warning` | String (Int) | Warning threshold (% used) | `75` |
| `device-checker-storage-critical` | String (Int) | Critical threshold (% used) | `90` |
| `device-checker-battery-enabled` | String (YES/NO) | Show battery-health tile | `YES` |
| `device-checker-thermal-enabled` | String (YES/NO) | Show thermal state tile | `YES` |
| `device-checker-performance-enabled` | String (YES/NO) | Show memory/CPU performance tile | `YES` |
| `device-checker-memory-warning` | String (Int) | Memory warning threshold (%) | `70` |
| `device-checker-memory-critical` | String (Int) | Memory critical threshold (%) | `85` |
| `device-checker-cpu-warning` | String (Int) | CPU warning threshold (%) | `60` |
| `device-checker-cpu-critical` | String (Int) | CPU critical threshold (%) | `80` |
| `device-checker-wifi-enabled` | String (YES/NO) | Show Wi-Fi connectivity tile | `YES` |
| `device-checker-cellular-enabled` | String (YES/NO) | Show cellular connectivity tile | `NO` |

### Network & Connectivity Tests

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-network-speed-enabled` | String (YES/NO) | Enable network speed test | `NO` |
| `device-checker-internet-connectivity-test-enabled` | String (YES/NO) | Enable internet reachability test | `NO` |
| `device-checker-internet-connectivity-test-endpoint` | String (URL) | Endpoint to test reachability against | `http://captive.apple.com/hotspot-detect.html` |
| `device-checker-internet-connectivity-test-timeout` | String (Int) | Test timeout in seconds | `3` |
| `device-checker-internet-connectivity-test-cache-ttl` | String (Int) | Cache result for N seconds | `30` |

### Alerts, Links & Sharing

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-alerts-url` | String (URL) | External alerts page shown inside the app | — |
| `device-checker-links-enabled` | String (YES/NO) | Enable custom quick-links section | `NO` |
| `device-checker-links-list` | String (JSON) | JSON array: `[{"title":"…","url":"…"}]` | — |
| `device-checker-send-status-enabled` | String (YES/NO) | Show "Send Status" share button | `YES` |
| `device-checker-send-logs-enabled` | String (YES/NO) | Show "Send Logs" share button | `YES` |

### Jamf Setup Extension Attribute

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-jamf-setup-ea-enabled` | String (YES/NO) | Show Jamf Setup duty status at the top of the app | `NO` |
| `device-checker-jamf-setup-ea-name` | String | Extension attribute name | `Jamf Setup` |
| `device-checker-jamf-setup-ea-on-duty-value` | String | Value that indicates on-duty | `On-duty` |
| `device-checker-jamf-setup-ea-off-duty-value` | String | Value that indicates off-duty | `Off-duty` |

### Auto-Refresh

| Key | Type | Description | Default |
|---|---|---|---|
| `device-checker-auto-refresh-threshold` | String (Int) | Minimum seconds between auto-refreshes on app activation (`0` disables throttling, range `60`–`3600`) | `300` |

For a working sample payload, see [`DeviceCheckerAppConfigSample`](https://github.com/Jamf-Concepts/jamf-device-checker/blob/main/DeviceCheckerAppConfigSample) in the source repository.
