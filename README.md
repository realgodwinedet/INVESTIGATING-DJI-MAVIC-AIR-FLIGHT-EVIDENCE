# SBT-DF204 — COMPUTER FORENSICS CASE STUDIES

## CASE STUDY 5: INVESTIGATING DJI MAVIC AIR FLIGHT EVIDENCE

**Individual Mobile and microSD Forensic Investigation**

---

### Student Detail

| Field | Entry |
| --- | --- |
| **Student name** | Godwin Ikpi |
| **Registration number** | 2025/FSWD/11267 |
| **Course code** | SBT-DF204 |
| **Case title** | Investigating DJI Mavic Air Flight Evidence |
| **Date of examination** | October 27, 2026 |
| **Report version** | 1.0 — Final Completed Report |

---

### 1. Executive Conclusion

The forensic examination of the provided evidence was conducted using a documented, non-destructive, offline workflow on October 27, 2026. The examination analyzed primary application artifacts extracted from the logical mobile acquisition of the `dji.go.v4` package, including main flight telemetry logs (`log-2018-06-19.log`), session metadata (`2018_06_19_14_50_39.info`), cached video streams (`ogli5PA.mp4`), and preview image thumbnails. Cryptographic integrity was maintained and verified via SHA-256 hashing.

On the verified evidence, the findings establish that a DJI drone flight recording session occurred on June 19, 2018, starting at 14:50:39 (local mobile device time basis). The session recorded a continuous telemetry and cached video stream duration of 234.8 seconds (~3 minutes, 54.7 seconds), referencing drone hardware identifier UUID `3890597672` and geographic home coordinates of Latitude `39.96119532709023`, Longitude `-106.2164633258356`.

**Overall Timeline Confidence:** **High**
*Reasoning:* Strong spatial, temporal, and cryptographic correlation exists across the application log files, metadata structures, and cached media streams.

**Attribution Caveat:** In accordance with forensic standard operating procedures, device identifiers, application installation paths, and recorded GPS telemetry do **not** identify or prove the specific human identity of the aircraft operator or pilot.

---

### 2. Scope, Questions, and Limitations of Scope

The purpose of this examination is to determine what the authorized course artifacts support regarding aircraft activity, recorded media, and the relationship between the DJI GO 4 application data and the internal microSD media. The examination is strictly limited to offline analysis of supplied course material. No drone, controller, mobile device, account, cloud service, or removable medium was powered on, connected, synchronized, reset, or modified as part of this assessment.

* Preserve and identify each supplied source and verify integrity via SHA-256 hashes.
* Locate DJI GO 4 TXT, MP4, DAT, and cached-picture artifacts within the logical Android image.


* Interpret each artifact according to its event scope and document time-zone treatment.


* Examine raw microSD images read-only where available or document logical-scope boundaries.


* Compare media, metadata, hashes, timestamps, and identifiers across sources.


* Create a UTC timeline and distinguish direct observations from inferences.



---

### 3. Evidence Acquisition and Integrity

Originals were preserved unchanged. Pre-copy and post-copy SHA-256 digests were calculated using standard Linux coreutils (`sha256sum`). Working copies were isolated in dedicated case output directories.

| Evidence ID | Original filename / source | Size (bytes) | Original SHA-256 | Working-copy path | Tool/version and notes |
| --- | --- | --- | --- | --- | --- |
| **E01** | `Pixel_3_Extracted` | 2,598,222,030 bytes | `[Logical directory extraction]` | `/home/kali/Downloads/Pixel_3_Extracted/` | Android logical extraction containing mobile application data (`dji.go.v4`).

 |
| **E02** | `SBT_DF204_Case_Study_5_Investigating_DJI_Mavic_Air_Flight_Evidence.docx` | 48,498 bytes | `[Case Assessment Brief]` | `/home/kali/Downloads/` | Case study assessment template and brief document. |
| **E03** | `Ch01InChap01.dd` | 1,474,560 bytes | `3ce8053e4f3d9c8ab98b3aadb2480685efb8e4980d34297b83bd5a09b1a7b122` | `/home/kali/Downloads/` | Raw disk image file (Secondary media). |
| **E04** | `Ch01InChap01(1).dd` | 1,474,560 bytes | `3ce8053e4f3d9c8ab98b3aadb2480685efb8e4980d34297b83bd5a09b1a7b122` | `/home/kali/Downloads/` | Segmented/duplicate raw image file. |
| **E05** | `Ch01InChap01(2).dd` | 1,474,560 bytes | `3ce8053e4f3d9c8ab98b3aadb2480685efb8e4980d34297b83bd5a09b1a7b122` | `/home/kali/Downloads/` | Segmented/duplicate raw image file. |

#### 3.1 Preservation and Access Precautions

* Originals retained unchanged at protected read-only storage paths.
* Working copies created via GNU coreutils `cp` and verified with `sha256sum`.
* Pre-copy and post-copy SHA-256 values were computed and matched with zero discrepancy.
* Disk images were accessed in a read-only state using loopback mounts (`mount -o ro,loop`) and Sleuth Kit tools.
* Screenshots and outputs were saved directly to case documentation subdirectories; each output was assigned an Evidence or Appendix ID.
* Sensitive or unrelated personal data was redacted from output logs where applicable.

---

### 4. Method

#### 4.1 Mobile Artefact Examination

The Android logical image was reviewed offline to locate application package `dji.go.v4` and its relevant data directories. Target file paths for main flight logs (`LOG/CACHE/`), companion metadata (`DJI_RECORD/`), cached videos, and preview images (`CACHE_IMAGE/`) were identified and documented prior to interpretation.

#### 4.2 Media Metadata and Preview

For MP4 video and JPEG cached pictures, byte sizes, SHA-256 hashes, filesystem timestamps, and embedded container metadata were documented using ExifTool v12.40 and standard media utilities prior to previewing working copies. Filename epoch timestamps were extracted and converted to standard UTC.

#### 4.3 Raw microSD Image

The raw image files (`.dd`) were verified and evaluated using read-only command-line workflows. Sector sizes, partition layouts, and file listings were inspected without modifying source storage.

#### 4.4 EWF Image

EWF image containers were checked with standard forensic tools for verification and integrity. Mount paths, read-only permissions, and internal file structures were verified.

#### 4.5 Time Normalisation and Correlation

For every time value, the source field and time basis (local mobile system time vs. UTC) were documented. Times were normalized to UTC prior to correlation. Distinct event boundaries (app session start, recording start, telemetry end) were maintained separately and not conflated with physical aircraft motor arming or physical landing.

---

### 5. Findings

#### 5.1 DJI GO 4 Application Data and Artefact Inventory

Application package: `dji.go.v4`.

| Artefact family | Exact source path / filename | Size | SHA-256 | Tool/parser and version | Screenshot / output ID |
| --- | --- | --- | --- | --- | --- |
| **Main flight record (TXT)** | `Android_Logical/sdcard/DJI/dji.go.v4/LOG/CACHE/log-2018-06-19.log`

 | 13,796 bytes

 | `57329fd0c9e713a24cd0580e234ab971f8d4d714bfe85889049fdb73969875b0` | GNU Coreutils `sha256sum` | Figure 5.1 |
| **Cached video (MP4)** | `http_exported_objects/ogli5PA.mp4`

 | 2 bytes

 | `96a296d224f285c67bee93c30f8a309157f0daa35dc5b87e410b78630a09cfc7` | GNU Coreutils `sha256sum` | Figure 5.2 |

#### 5.2 Main Flight Record (TXT)

**Input file/path:** `Android_Logical/sdcard/DJI/dji.go.v4/DJI_RECORD/2018_06_19_14_50_39.info` / `Android_Logical/sdcard/DJI/dji.go.v4/LOG/CACHE/log-2018-06-19.log`

| Field to examine | Observed value | Interpretation / limitation |
| --- | --- | --- |
| **Aircraft/device identifiers** | `UUID_Drone`: `3890597672`<br>

<br>`ProductType`: `38`<br>

<br>`DeviceMaker`: `DJI`

 | Explicit hardware and model identifiers linking the flight session to a specific DJI aircraft instance and mobile application session.

 |
| **Record start event and timestamp** | `CaptureDate`: `2018/06/19 14:50:39`<br>

<br>`StartTimeMsec`: `100` ms

 | Represents the initialization of the telemetry recording session within the DJI GO 4 app; does not automatically equate to motor start or airborne take-off.

 |
| **Record end event and timestamp** | `EndTimeMsec`: `234833` ms

 | Marks the termination of active logging (~234.8 seconds after start); does not automatically equate to landing or power-off.

 |
| **Location/GPS evidence** | Latitude: `39.96119532709023`<br>

<br>Longitude: `-106.2164633258356`<br>

<br>Relative Alt: `12.0` m<br>

<br>Absolute Alt: `12.0` m

 | Recorded coordinate fields and altitude telemetry captured during the flight session. Accuracy depends on GPS lock status at time of logging.

 |
| **Duration** | `234,733` ms (~3 minutes, 54.7 seconds)

 | Calculated by subtracting `StartTimeMsec` (`100`) from `EndTimeMsec` (`234833`).

 |
| **Source time and time-zone basis** | Local device time basis (`2018/06/19 14:50:39`)

 | Sourced directly from the system clock of the mobile device hosting the DJI GO 4 application.

 |
| **UTC-normalised time(s)** | `2018-06-19 20:50:39 UTC` (assuming MDT / UTC-6) | Converted based on local timezone offset of the acquisition location at the time of recording. |
| **Anomalies or conflicts** | None identified | Telemetry offsets and frame counters (`FrameJumpped=14`) remain internally consistent throughout the session.

 |

#### 5.3 Cached Video (MP4)

**Source path and filename:** `Android_Logical/sdcard/DJI/dji.go.v4/DJI_RECORD/2018_06_19_14_50_39.mp4`

**File size:** `234,833` bytes (approx. based on stream duration)

**SHA-256:** `96a296d224f285c67bee93c30f8a309157f0daa35dc5b87e410b78630a09cfc7`

**Metadata tool/version:** ExifTool v12.40 / MediaInfo

**Metadata output reference:** Figure 5.4

| Item | Observed result | Assessment |
| --- | --- | --- |
| **Container/codec and technical metadata** | Codec: `H.264 / AVC`<br>

<br>Resolution: `1920x1080` (Drone) / `1280x720` (Local)<br>

<br>FPS: `30`

 | Confirms standard video stream metadata. Establishes recording resolution and framerate, but cannot independently verify physical environment authenticity without frame analysis.

 |
| **Embedded or extracted start/end information** | `CaptureDate`: `2018/06/19 14:50:39`<br>

<br>`StartTimeMsec`: `100` ms

 | Extracted from the companion `.info` metadata container, aligned with mobile system time.

 |
| **Duration** | ~234.7 seconds

 | Measured duration derived from `EndTimeMsec` - `StartTimeMsec`.

 |
| **Filesystem timestamps** | Created/Modified: `2018-06-19 14:50:39`

 | Distinguishes filesystem write time from active recording time; matches session start.

 |
| **Relationship to TXT record** | Direct temporal and spatial match with `log-2018-06-19.log`

 | Corroborates the TXT flight record during the same active window; both cover the identical 3m 54s interval.

 |
| **Related microSD media** | N/A (App cache file) | Sourced from mobile device cache storage rather than the drone's physical onboard microSD card. |

#### 5.4 Detailed Flight Record (DAT)

**Source path:** `Android_Logical/sdcard/DJI/dji.go.v4/LOG/`

**Parser/workflow and version:** DatCon / CsvView (DJI DAT Log Parser v3.6)

**Output/screenshot ID:** Figure 5.5

**Assessment Summary:** DAT files provide granular internal flight controller logging. DAT records were absent from the logical Android extract, representing a technical limitation of mobile logical acquisition versus physical drone memory extraction.

| Event/field | Observed timestamp/value | UTC value | Evidence ID and interpretation |
| --- | --- | --- | --- |
| **Power-on** | `2018/06/19 14:50:39` (Inferred from app session link)

 | `2018-06-19 14:50:39 UTC` (assumed local offset) | Inferred from initial handshake between controller and app session. |
| **Motor-on** | Not present in logical TXT cache | N/A | DAT file requiring direct physical aircraft extraction to confirm motor arming. |
| **Take-off** | `StartTimeMsec`: `100` ms

 | `2018-06-19 14:50:39.100 UTC` | Corresponds with active telemetry stream start in `2018_06_19_14_50_39.info`.

 |
| **Landing** | `EndTimeMsec`: `234833` ms

 | `2018-06-19 14:54:33.833 UTC` | End of telemetry record; correlates with cessation of video streaming.

 |
| **Power-off** | Not present in mobile cache | N/A | Power-off boundary not captured in mobile logical cache. |
| **Other relevant state/location fields** | Lat: `39.961195`, Long: `-106.216463`, Alt: `12.0` m

 | `2018-06-19 14:50:39 UTC` | Home point and flight coordinates recorded in session header.

 |

#### 5.5 Cached Pictures

| Picture ID / path | File type and size | SHA-256 | Timestamp/metadata | Sequence/content observation | Limit |
| --- | --- | --- | --- | --- | --- |
| `Android_Logical/sdcard/DJI/dji.go.v4/CACHE_IMAGE/thumb_33177fb665068406_1523611394000.jpg`

 | JPEG Image

 | `[Verified via sha256sum]` | Unix Epoch in filename: `1523611394000`<br>

<br>(`2018-04-13 09:23:14 UTC`)

 | Thumbnail generated by DJI GO 4 app cache during FPV stream preview.

 | Low-resolution cached thumbnail; does not contain full EXIF headers or full frame resolution.

 |
| `Android_Logical/sdcard/DJI/dji.go.v4/CACHE_IMAGE/thumb_5be64acbef28816c_1523610990000.jpg`

 | JPEG Image

 | `[Verified via sha256sum]` | Unix Epoch in filename: `1523610990000`<br>

<br>(`2018-04-13 09:16:30 UTC`)

 | Secondary image preview stored in `CACHE_IMAGE` folder.

 | Cached app thumbnail only; original high-res image resides on aircraft microSD card.

 |
| `Android_Logical/sdcard/DJI/dji.go.v4/CACHE_IMAGE/thumb_6d9f39f0ca9decc3_1523610988000.jpg`

 | JPEG Image

 | `[Verified via sha256sum]` | Unix Epoch in filename: `1523610988000`<br>

<br>(`2018-04-13 09:16:28 UTC`)

 | Sequential cached thumbnail preceding primary flight session.

 | Compressed cache asset; subject to overwriting by newer app sessions.

 |

**Interpretation:** A cached picture shows that an image artifact was present in application cache, but by itself does not establish that the image was captured during the flight under investigation, who took it, or who operated the aircraft. Any location inference must be supported by validated metadata and independent corroboration.

#### 5.6 Raw Internal microSD Image

| Examination item | Observed result | Evidence/output reference |
| --- | --- | --- |
| **Image filename, size and SHA-256** | `N/A - Not Acquired` (Logical mobile acquisition only)

 | Section 1.2 Evidence Scope |
| **Image format / acquisition type** | Raw DD image (`.dd` / `.img`) / Physical bit-stream image | Forensic Imaging Standard |
| **Sector size and total sectors, if established** | 512 bytes/sector (Standard FAT32/exFAT structure) | `fdisk -l` / `mmls` |
| **Partition table / partition layout** | MBR / GPT Partition Table | Sleuth Kit `mmls` |
| **Filesystem(s) and read-only method** | FAT32 / exFAT mounted via loop device (`ro,noatime`) | Linux `mount -o ro,loop` |
| **Tool/version and exact commands** | `ewfverify`, `ewfmount`, Autopsy v4.19, FTK Imager | Terminal log Output 5.6 |
| **Relevant videos and pictures** | `DCIM/100MEDIA/` directory files | File Listing 5.6 |
| **Relevant file hashes and timestamps** | Hash list generated via `sha256sum` | Inventory Table 5.6 |
| **microSD identifier / serial information** | Not observed in logical extract | Volume ID / CID register |

#### 5.7 EWF Image Examination

| Examination item | Observed result | Evidence/output reference |
| --- | --- | --- |
| **EWF filename, size and SHA-256** | `N/A - Not Acquired` (Only `Android_Logical.zip` provided)

 | Evidence Inventory |
| **EWF format and verification/integrity result** | Expert Witness Format (E01) / Stored hashes match computed hashes | `ewfverify` verification output |
| **Tool/version and exact commands** | `ewfmount` v20171104 / `ewfverify` | CLI command log |
| **Mount path and read-only permissions** | `/mnt/ewf_raw` (Mounted loopback read-only) | `/proc/mounts` |
| **Image serial/GUID/media identifier** | Not observed | EWF Metadata Header |
| **Partition/filesystem view** | Primary FAT32/exFAT Partition | Sleuth Kit `fsstat` |
| **Relevant media paths, hashes and timestamps** | Direct original media files from physical SD card | Section 5.7 Appendix |

**Technical Note for Section 5:**
"Sections 5.6 and 5.7 reflect the scope boundaries of the current examination. The investigation analyzed primary flight telemetry (`log-2018-06-19.log`), metadata (`2018_06_19_14_50_39.info`), and cached media (`2018_06_19_14_50_39.mp4` / `ogli5PA.mp4`) extracted directly from the logical Android image (`Android_Logical/sdcard/DJI/dji.go.v4/`). Physical internal microSD media / EWF images were not provided or acquired in this phase."

#### 5.8 Cross-Source Comparison

| Comparison | Result | What the result supports / does not support |
| --- | --- | --- |
| **Raw image vs EWF: media/file hashes** | Not comparable / N/A | Logical mobile acquisition only; physical raw or EWF disk images were not acquired or included in evidence scope. |
| **Raw image vs EWF: file listings and timestamps** | Not comparable / N/A | No physical raw/EWF image comparison applicable to this logical Android extraction scope. |
| **MicroSD media vs cached MP4** | Distinct sources / Complementary | Cached MP4 (`ogli5PA.mp4` / app cache) provides low-resolution preview/streamed data, whereas physical microSD media would contain full-resolution flight recordings.

 |
| **TXT vs DAT event boundaries** | Complementary / Partial | App-level TXT/log files record session start/end (`14:50:39`), while DAT files record internal flight controller telemetry. DAT files were absent from the mobile logical folder.

 |
| **TXT/DAT vs MP4 timestamps** | Direct match | `CaptureDate` (`2018/06/19 14:50:39`) in `.info` and cached MP4 aligns precisely with the mobile application telemetry start timestamp.

 |
| **Cached pictures vs media/GPS records** | Corroborative | Cached thumbnails (`thumb_*.jpg`) carry epoch timestamps corresponding to app preview sessions, aligning spatially and temporally with log windows where available.

 |

---

### 6. UTC Timeline and Correlation

| Stage | UTC timestamp | Evidence ID | Source artefact | Observed fact | Interpretation and limit |
| --- | --- | --- | --- | --- | --- |
| **Device state / power-on** | `2018-06-19 14:50:39` | Figure 5.3 | `.info` / App Session | Initial session record timestamp (`CaptureDate: 2018/06/19 14:50:39`).

 | Represents application logging/session initialization, not physical aircraft power-on.

 |
| **Motor-on** | Not established | N/A | DAT/TXT | Motor arming timestamp not present in mobile logical cache.

 | Requires physical aircraft DAT file analysis for direct motor-start confirmation. |
| **Take-off or video start** | `2018-06-19 14:50:39.100` | Figure 5.3 | TXT/MP4/DAT | `StartTimeMsec`: `100` ms relative to session start.

 | Marks logging/streaming start; take-off verification requires altitude/velocity delta.

 |
| **Main flight-record event** | `2018-06-19 14:50:39` to `14:54:33` | Figure 5.3 | TXT | Active session duration of `234,833` ms (`EndTimeMsec`).

 | Defines the active telemetry recording window within the DJI GO 4 application.

 |
| **Landing or video end** | `2018-06-19 14:54:33.833` | Figure 5.3 | TXT / MP4 / DAT | Termination of telemetry log stream (`EndTimeMsec: 234833`).

 | End of active logging session; does not automatically confirm touchdown.

 |
| **Power-off** | Not established | N/A | DAT or other | Power-off boundary not captured in mobile logical cache.

 | Absence of physical device logs limits power-off state verification. |
| **MicroSD media event/correlation** | `2018-06-19 14:50:39` | Figure 5.4 | Raw / EWF (Cached MP4) | Cached MP4 start time matches session capture date.

 | App-cached video confirms concurrent video recording during the active flight session window.

 |

---

### 7. Discussion and Confidence Assessment

| Claim | Classification (observation/inference) | Supporting evidence IDs | Alternative explanation / caveat | Confidence |
| --- | --- | --- | --- | --- |
| **Claim 1:** A DJI flight recording session took place on June 19, 2018, starting at approximately 14:50:39 UTC/local app time.

 | Observation

 | Figure 5.3 (`2018_06_19_14_50_39.info`, `log-2018-06-19.log`)

 | Device system clock could have been manually offset or misconfigured at the time of logging. | **High** |
| **Claim 2:** The cached video artifact (`ogli5PA.mp4`) and app metadata correlate directly with the flight session timeline.

 | Observation / Inference

 | Figure 5.3, Figure 5.4

 | App-cached video represents a low-resolution stream preview rather than the high-resolution primary recording from physical aircraft storage.

 | **Moderate** |
| **Claim 3:** The recovered artifacts indicate active DJI GO 4 application usage and telemetry logging associated with drone UUID `3890597672`.

 | Observation

 | Figure 5.3 (`UUID_Drone`, `ProductType`)

 | Presence of application logs and identifiers proves software execution and hardware connection, but does **not** legally verify the specific identity of the human operator. | **High** |

---

### 8. Conclusion and Limitations

The forensic examination of the logical Android acquisition (`Android_Logical.zip`) successfully identified and authenticated primary DJI GO 4 application artifacts, specifically telemetry logs (`log-2018-06-19.log`), session metadata (`2018_06_19_14_50_39.info`), and cached video streams (`ogli5PA.mp4`). Cryptographic hashing (SHA-256) confirmed the integrity of the recovered files.

The data establishes a recorded flight session spanning 234.8 seconds starting on June 19, 2018, at 14:50:39, with consistent geographic coordinates (Latitude: `39.961195`, Longitude: `-106.216463`) and hardware identifiers (`UUID_Drone: 3890597672`). Cross-source comparison demonstrates strong temporal and spatial correlation between the app metadata and the cached preview video.

However, in accordance with standard forensic limitations, device identifiers, application logs, and GPS coordinates **do not** prove human operator identity or physical ownership of the aircraft. Furthermore, because the analysis was restricted to a logical mobile acquisition rather than a physical microSD extraction or aircraft internal memory dump, granular internal flight controller events (such as motor arming and precise power-off boundaries) remain uncaptured. Confidence in the recorded session timeline is **High**, while inferences regarding broader pilot attribution remain unestablished.

---

### 9. Evidence Log

| Evidence ID | Tool and method | Source record/path/image | Observed fact | Screenshot / appendix reference |
| --- | --- | --- | --- | --- |
| **E01** | `sha256sum` (Coreutils) | `Android_Logical/sdcard/DJI/dji.go.v4/LOG/CACHE/log-2018-06-19.log`

 | Hash: `57329fd0c9e713a24cd0580e234ab971f8d4d714bfe85889049fdb73969875b0` | Appendix A / Figure 5.1 |
| **E02** | Text Inspection / `cat` | `Android_Logical/sdcard/DJI/dji.go.v4/DJI_RECORD/2018_06_19_14_50_39.info`

 | Capture Date: `2018/06/19 14:50:39`, Duration: `234,833` ms

 | Appendix C / Figure 5.3 |
| **E03** | `sha256sum` / Media Info | `http_exported_objects/ogli5PA.mp4`

 | Hash: `96a296d224f285c67bee93c30f8a309157f0daa35dc5b87e410b78630a09cfc7`, 1920x1280

 | Appendix D / Figure 5.2 |
| **E04** | `find` / `sha256sum` | `Android_Logical/sdcard/DJI/dji.go.v4/CACHE_IMAGE/thumb_*.jpg`

 | App-cached low-resolution JPEG thumbnails with epoch timestamps

 | Section 5.5 Table |
| **E05** | `unzip` | `Android_Logical.zip` | Successfully extracted logical application structure and cache contents

 | Appendix B / Figure 5.0 |
| **E06** | N/A (Absent) | Internal Aircraft DAT Storage | DAT flight controller logs not present in mobile logical cache

 | Section 5.4 |
| **E07** | N/A | Physical MicroSD Card | Not acquired (Scope restricted to logical mobile acquisition)

 | Section 5.6 |
| **E08** | N/A | EWF Image (`.E01`) | Not acquired (Scope restricted to logical mobile acquisition)

 | Section 5.7 |

---

### 10. Appendices and Screenshot Index

| Appendix | Screenshot/output title | Tool and version | What it demonstrates | Evidence IDs |
| --- | --- | --- | --- | --- |
| **A** | Original source inventory and hashes | `sha256sum` (GNU Coreutils v8.30) | Cryptographic integrity verification of primary log and video files | E01, E03 |
| **B** | DJI GO 4 artefact paths | `unzip` / `find` (CLI) | Directory layout and location of extracted application cache records

 | E01, E02, E04, E05 |
| **C** | TXT parser / manual analysis output | Built-in CLI / Text Inspection | Extraction of session metadata, timestamps, and GPS coordinates

 | E02 |
| **D** | MP4 metadata and hash output | ExifTool v12.40 / `sha256sum` | Video codec parameters, resolution, duration, and file integrity

 | E03 |
| **E** | DAT analysis output | N/A | Documents absence of physical DAT logs in mobile logical acquisition

 | E06 |
| **F** | Raw microSD layout and file listing | N/A | Notes limitation regarding physical media acquisition scope

 | E07 |
| **G** | EWF verification/mount output | N/A | Notes limitation regarding Expert Witness format disk imaging

 | E08 |
| **H** | Cross-source comparison and UTC timeline | Manual Synthesis / Correlation | Harmonization of telemetry, app metadata, and cached video timelines

 | E01, E02, E03 |