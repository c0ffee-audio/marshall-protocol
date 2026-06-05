# Marshall Bluetooth Protocol

Reverse-engineered BLE protocol for Zound Industries / Marshall Bluetooth devices.

Derived from static analysis of the Marshall Bluetooth Android app (`com.zoundindustries.marshallbt`), version 3.7.1.

## Devices

- Marshall Motif II ANC (earbuds)
- Marshall Willem (speaker)
- Marshall Major IV, Monitor III ANC, and others using the same `bleprotocol` library

## UUID Schemes

Three UUID bases are used depending on the device generation and feature:

| Scheme | Format | Use |
|--------|--------|-----|
| Zound proprietary (current) | `0000{code}-1337-1dea-feed-c0ffee70c0de` | All modern features |
| Zound legacy | `0000{legacyCode}-0000-1000-8000-00805f9b34fb` | Older firmware |
| Bluetooth standard | `0000{code}-0000-1000-8000-00805f9b34fb` | Battery, device info |
| Qualcomm GAIA (OTA) | `0000{code}-d102-11e1-9b23-00025b00a5a5` | Firmware update |

The modern Zound UUID suffix (`-1337-1dea-feed-c0ffee70c0de`) is an easter egg: 1337 (leet), 1dea (idea), feed, c0ffee (coffee).

## Primary Service UUID

`FA302D24-D775-4343-B9ED-8CC68ACE3284`

## GATT Characteristics

### Device Information (Bluetooth Standard)

| Name | UUID | Type |
|------|------|------|
| MANUFACTURER_NAME | `00002a29-0000-1000-8000-00805f9b34fb` | Read |
| MODEL_NAME | `00002a24-0000-1000-8000-00805f9b34fb` | Read |
| SERIAL_NUMBER | `00002a25-0000-1000-8000-00805f9b34fb` | Read |
| FIRMWARE_REVISION | `00002a26-0000-1000-8000-00805f9b34fb` | Read |
| HARDWARE_REVISION | `00002a27-0000-1000-8000-00805f9b34fb` | Read |
| BATTERY_LEVEL | `00002a19-0000-1000-8000-00805f9b34fb` | Read/Notify |
| BATTERY_LEVEL_STATUS | `00002bed-0000-1000-8000-00805f9b34fb` | Read/Notify |

### Zound Proprietary Characteristics

| Name | Code | UUID | Legacy UUID | Type |
|------|------|------|-------------|------|
| BLUETOOTH_CLASSIC_PAIRING_MODE | 0001 | `00000001-1337-1dea-feed-c0ffee70c0de` | `0000aa02-...` | Read/Write |
| RENAME | 0003 | `00000003-1337-1dea-feed-c0ffee70c0de` | `0000aa04-...` | Read/Write |
| AUTO_POWER_OFF | 0004 | `00000004-1337-1dea-feed-c0ffee70c0de` | `0000aa05-...` | Read/Write |
| VOLUME | 0007 | `00000007-1337-1dea-feed-c0ffee70c0de` | `0000aa08-...` | Read/Write/Notify |
| VOLUME_LIMIT | 0008 | `00000008-1337-1dea-feed-c0ffee70c0de` | `0000aa09-...` | Read/Write |
| AUDIO_CONTROL | 0009 | `00000009-1337-1dea-feed-c0ffee70c0de` | `0000aa10-...` | Write |
| AUDIO_NOW_PLAYING | 000a | `0000000a-1337-1dea-feed-c0ffee70c0de` | `0000aa11-...` | Read/Notify |
| UI_SOUNDS | 000b | `0000000b-1337-1dea-feed-c0ffee70c0de` | `0000aa12-...` | Read/Write |
| ACTION_BUTTON_EVENT | 000c | `0000000c-1337-1dea-feed-c0ffee70c0de` | `0000aa13-...` | Notify |
| ACTION_BUTTON_CONFIGURATION | 000d | `0000000d-1337-1dea-feed-c0ffee70c0de` | `0000aa14-...` | Read/Write |
| GRAPHICAL_EQUALIZER | 000f | `0000000f-1337-1dea-feed-c0ffee70c0de` | `0000aa16-...` | Read/Write |
| ANC_CONFIGURATION | 0013 | `00000013-1337-1dea-feed-c0ffee70c0de` | `0000aa20-...` | Read/Write/Notify |
| TOUCH_LOCK | 0014 | `00000014-1337-1dea-feed-c0ffee70c0de` | `0000aa21-...` | Read/Write |
| EQUALIZER_SETTINGS | 0017 | `00000017-1337-1dea-feed-c0ffee70c0de` | `0000aa25-...` | Read/Write |
| EQUALIZER_SETTINGS_CUSTOM_PRESET | 0018 | `00000018-1337-1dea-feed-c0ffee70c0de` | `0000aa26-...` | Read/Write |
| ANC_TRANSPARENCY_VALUE | 0019 | `00000019-1337-1dea-feed-c0ffee70c0de` | `0000aa27-...` | Read/Write |
| ANC_NOISE_CANCELLING_VALUE | 001a | `0000001a-1337-1dea-feed-c0ffee70c0de` | `0000aa28-...` | Read/Write |
| AUDIO_SOURCE | 001b | `0000001b-1337-1dea-feed-c0ffee70c0de` | `0000aa29-...` | Read/Write |
| PARTY_MODE | 001c | `0000001c-1337-1dea-feed-c0ffee70c0de` | `0000aa2a-...` | Read/Write |
| ECO_CHARGING | 001d | `0000001d-1337-1dea-feed-c0ffee70c0de` | `0000aa2b-...` | Read/Write |
| ROOM_PLACEMENT | 001e | `0000001e-1337-1dea-feed-c0ffee70c0de` | `0000aa2c-...` | Read/Write |
| NIGHT_MODE | 001f | `0000001f-1337-1dea-feed-c0ffee70c0de` | `0000aa2d-...` | Read/Write |
| TONE_CONTROL | 0025 | `00000025-1337-1dea-feed-c0ffee70c0de` | `0000aa33-...` | Read/Write |
| WEAR_SENSOR_STATUS | 0027 | `00000027-1337-1dea-feed-c0ffee70c0de` | - | Read/Notify |
| WEAR_SENSOR_ACTION | 0028 | `00000028-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| BATTERY_PRESERVATION | 002f | `0000002f-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| DYNAMIC_AUDIO | 0030 | `00000030-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| AUTO_OFF_TIMER | 0032 | `00000032-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| SOUNDSTAGE | 0033 | `00000033-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| BT_CONNECTION_CONTROL | 0034 | `00000034-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| LED_INTENSITY | 003a | `0000003a-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| LE_AUDIO_CONFIG | 003d | `0000003d-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| AUDIO_FEATURE_CONFIG | 0044 | `00000044-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| AUDIO_INPUT_FEATURE_CONFIG | 0045 | `00000045-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |
| USB_CONFIG | 0048 | `00000048-1337-1dea-feed-c0ffee70c0de` | - | Read/Write |

### Earbuds Battery (Tymphany SDK UUIDs)

| Name | UUID |
|------|------|
| RIGHT_EARBUD_BATTERY_LEVEL | `7a573e5d-9330-4d9b-8660-63c33fc50001` |
| LEFT_EARBUD_BATTERY_LEVEL | `7a573e5d-9330-4d9b-8660-63c33fc50002` |
| MAIN_CASE_BATTERY_LEVEL | `7a573e5d-9330-4d9b-8660-63c33fc50003` |
| RIGHT_EARBUD_BATTERY_LEVEL_STATUS | `7a573e5d-9330-4d9b-8660-63c33fc50101` |
| LEFT_EARBUD_BATTERY_LEVEL_STATUS | `7a573e5d-9330-4d9b-8660-63c33fc50102` |
| MAIN_CASE_BATTERY_LEVEL_STATUS | `7a573e5d-9330-4d9b-8660-63c33fc50103` |

## Command Encodings

### ANC_CONFIGURATION (`00000013-1337-1dea-feed-c0ffee70c0de`)

Single byte write:

| Value | Mode |
|-------|------|
| `0x00` | Playback only (ANC off) |
| `0x01` | Active Noise Cancelling |
| `0x02` | Transparency / Ambient |

### EQ Presets — EQUALIZER_SETTINGS (`00000017-1337-1dea-feed-c0ffee70c0de`)

Two writes are required to change the EQ preset:

1. `ASSIGN_STEP_PRESET`: `[0x01, stepIndex, presetId]` - assign preset to a step slot
2. `CHANGE_ACTIVE_STEP`: `[0x00, stepIndex]` - activate that step slot

There are 3 step slots (0, 1, 2). For a simple preset change, use step 0 both times.

Preset IDs (scheme 0, `EqStepPreset` in `EqSettingsCharacteristicWrapper`):

| Preset | ID |
|--------|----|
| FLAT | 0 |
| CUSTOM | 1 |
| ROCK | 2 |
| METAL | 3 |
| POP | 4 |
| HIPHOP | 5 |
| ELECTRONIC | 6 |
| JAZZ | 7 |
| BASS_BOOST | 8 |
| MID_BOOST | 9 |
| TREBLE_BOOST | 10 |
| LOUD_PUSH_WORKOUT | 11 |

Example: set EQ to ROCK - write `[0x01, 0x00, 0x02]` then `[0x00, 0x00]`.

### Features by Device

Features are assigned per `DeviceSubType`. The `Feature` enum includes:

- `ANC_MODE`, `ANC_CANCELLING`, `ANC_TRANSPARENCY`, `ADAPTIVE_ANC`, `ANC_TRA_4_LVL`
- `BATTERY`, `BATTERY_LEVEL`, `BATTERY_LEVEL_STATUS`, `EARBUDS_BATTERY_LEVEL`, `EARBUDS_WITH_CASE_BATTERY_LEVEL`
- `EQ_CUSTOM_SETTING`, `EQ_STEP_CHANGE`, `TWO_BAND_GRAPHICAL_EQ`, `TONE_CONTROL`, `CUSTOM_AIROHA_EQ`
- `VOLUME`, `VOLUME_LIMIT`, `PLAY_CONTROL`
- `TOUCH_LOCK`, `ACTION_BUTTON_EARBUDS`, `ACTION_BUTTON_HEADPHONES`
- `SOUNDSTAGE`, `DYNAMIC_AUDIO`, `NIGHT_MODE`, `LED_INTENSITY`
- `AUTO_OFF_TIMER`, `POWER_OFF_TIMER`, `ECO_CHARGING`, `BATTERY_PRESERVATION`
- `SPOTIFY_TAP`, `AUTO_PLAY_PAUSE`, `WEAR_SENSOR`
- `PARTY_MODE`, `RENAME`, `FORGET`, `SIMPLE_PAIRING`

## OTA / Firmware Update

Three OTA protocols are supported:

| Protocol | Used for |
|----------|----------|
| GAIA (Qualcomm) | Headphones with Qualcomm chip |
| Airoha | Earbuds with Airoha chip (Motif II ANC) |
| Tymphany/Joplin | Speakers (Willem, Stanmore, etc.) |

## Connection and Authentication

Devices like the Motif II ANC use **dual-mode Bluetooth**:

- **BR/EDR** (`public` address, e.g. `00:25:D1:41:DF:69`): A2DP audio, AVRCP
- **BLE** (`random` address, e.g. `C8:E0:09:EA:5B:AF`): GATT control (ANC, EQ, etc.)

The BLE address changes between sessions. Scan for devices with `AddressType=random` and match by name (`MOTIF II A.N.C. [LE]`).

### Pairing

Proprietary Zound characteristics require a BLE bond. The device accepts **Just Works** pairing (`NoInputNoOutput` capability). BlueZ requires an agent to be registered before calling `Pair()`:

```
RegisterAgent("/path/to/agent", "NoInputNoOutput")
RequestDefaultAgent("/path/to/agent")
Device1.Pair()
```

The device-side code (`ConnectivityManager`) calls `createBond()` on the BLE device after connection only when:
- The device type does not support `IMPLICIT_BOND`
- BLE is in `BOND_NONE` state
- BR/EDR is in `BOND_BONDED` state (CTKD scenario)

For SAXON (Motif II ANC), `IMPLICIT_BOND` is not listed - so the above logic triggers. In practice, a direct BLE Just Works pairing also works without a prior BR/EDR bond.

## Firmware / Chipsets

| Chipset | OTA Protocol | Observed on |
|---------|-------------|-------------|
| Airoha AB1565 | Airoha OTA | Motif II ANC (firmware: `IoT_SDK_for_BT_Audio_V3.4.1.AB1565_AB156`) |
| Qualcomm | GAIA | Major IV, Monitor III |
| Tymphany/Joplin | Joplin OTA | Willem, Stanmore, Woburn |

## Notes

- Modern devices support both the new (`-1337-1dea-...`) and legacy (`-00805f9b34fb`) UUID variants.
- Characteristics discovery should attempt the modern UUID first, then fall back to legacy.
- The app uses RxJava observable streams for characteristic notifications.
- `ServicesResolved=true` on the BR/EDR device path in BlueZ does NOT expose GATT characteristics - GATT is only available via the BLE connection.
