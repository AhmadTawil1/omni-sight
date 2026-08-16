# Datasets

All five datasets used by OmniSight, covering the three target domains
(surveillance, sports, traffic).

**Status legend:** ⬜ not started · 🔄 in progress · ✅ obtained & verified

| # | Dataset | Domain | Access | Size | Status | Owner |
|---|---------|--------|--------|------|--------|-------|
| 1 | DoTA | Traffic | Open — direct download | ~55 GB | ⬜ | |
| 2 | UCF-Crime | Surveillance | Open — direct download | ~120 GB | ⬜ | |
| 3 | AI City Challenge (Track 2) | Traffic | Open — no form required | TBC | ⬜ | |
| 4 | VIRAT | Surveillance | Free — account signup | ~70 GB | ⬜ | |
| 5 | SoccerNet | Sports | NDA form → password | Varies by task | ⬜ | |

> **Order of work:** submit the SoccerNet NDA first (only item with a waiting
> period), start the DoTA download in parallel (largest file), then the rest.
> The real constraint is **disk space and download time**, not approval.

---

## 1. DoTA — Detection of Traffic Anomaly

**Domain:** Traffic · **Role:** PFM traffic head · time-to-event and early-warning measurement (SM-3)

| Field | Value |
|---|---|
| **Licence** | MIT |
| **Size on disk** | ~55 GB (frames), split into 5 × 10 GB + 1 × 5 GB archives |
| **Access** | Open. No form, no approval. |
| **Download** | Pre-extracted frames from the authors' Google Drive (linked in the repo README) — this avoids the YouTube download + frame extraction pipeline entirely |
| **Source** | https://github.com/MoonBlvd/Detection-of-Traffic-Anomaly |
| **Approval time** | None |
| **Annotation format** | Per-video `.json`, plus `metadata_train.json` / `metadata_val.json` |

**Annotation fields:** `video_start`, `video_end`, `anomaly_start`, `anomaly_end`,
`anomaly_class`, `num_frames`, `subset`.

**Why it matters:** the only dataset with exact anomaly start/end frame numbers, so
it anchors SM-3 (≥ 15 s early-warning lead time) and precursor-window generation.

**Notes:**
- 4,677 video clips, 18 anomaly categories.
- Ego-centric (dash-cam) viewpoint.
- 6 long videos were removed from YouTube; the authors host them separately.
- Object bounding-box tracks and optical-flow features are available as an optional extra download.

**Checklist**
- [ ] Downloaded
- [ ] Extracted and verified
- [ ] Loader written
- [ ] Precursor windows generated

---

## 2. UCF-Crime

**Domain:** Surveillance · **Role:** PFM surveillance head · verification and false-positive evaluation (SM-4)

| Field | Value |
|---|---|
| **Licence** | Academic / research use |
| **Size on disk** | ~120 GB (confirm on download) |
| **Access** | Open — public download, no approval |
| **Download** | Official project page; Kaggle mirrors exist if the primary link is slow |
| **Source** | https://www.crcv.ucf.edu/projects/real-world/ |
| **Approval time** | None |
| **Annotation format** | Video-level labels; temporal annotations for the test split |

**Contents:** 1,900 untrimmed real-world CCTV videos, 128 hours, 13 anomaly classes
(Abuse, Arrest, Arson, Assault, Road Accident, Burglary, Explosion, Fighting,
Robbery, Shooting, Stealing, Shoplifting, Vandalism).

**Split:** train 800 normal + 810 anomalous · test 150 normal + 140 anomalous.

**⚠ Known limitation:** the standard release gives only **video-level** labels for the
training set — it does *not* mark when an anomaly begins. Precursor windows must be
derived semi-automatically and spot-checked by hand (Week 6, Task B).

**Checklist**
- [ ] Downloaded
- [ ] Extracted and verified
- [ ] Loader written
- [ ] Precursor windows generated

---

## 3. AI City Challenge — Track 2 (Traffic Safety Description and Analysis)

**Domain:** Traffic · **Role:** multi-camera forensic dossier validation (SM-6)

| Field | Value |
|---|---|
| **Licence** | Challenge terms — non-commercial research |
| **Size on disk** | TBC |
| **Access** | **Open — the data access request form is no longer required** and password protection has been removed |
| **Download** | Instructions on the individual track page under the CHALLENGE tab |
| **Source** | https://www.aicitychallenge.org/ai-city-challenge-dataset-access/ |
| **Approval time** | None for the dataset |
| **Annotation format** | Track-specific — confirm on the track page |

**Why it matters:** the **only** dataset with synchronised, overlapping multi-camera
coverage, so it is the sole basis for validating cross-camera correlation in the
RAG forensic dossier (SM-6, TC-7).

**Notes:**
- The 2024 and 2025 editions of Track 2 are both on the available list.
- Only the datasets explicitly listed on the access page remain available; others were retired.
- An evaluation-server account (separate from the data) requires an **institutional
  email** — personal Gmail addresses are not approved. Only needed if submitting to
  the leaderboard, which this project does not require.

**Checklist**
- [ ] Downloaded
- [ ] Extracted and verified
- [ ] Loader written
- [ ] Multi-camera scenarios identified

---

## 4. VIRAT

**Domain:** Surveillance · **Role:** ingestion and semantic-search evaluation (SM-1)

| Field | Value |
|---|---|
| **Licence** | Research use |
| **Size on disk** | ~70 GB (confirm on download) |
| **Access** | Free, but requires **account signup** — credentials issued on registration |
| **Download** | mevadata.org; also mirrored on Kitware's data portal and via NIST |
| **Source** | https://viratdata.org · https://actev.nist.gov · https://data.kitware.com |
| **Approval time** | Immediate to short — signup, not academic review |
| **Annotation format** | Object tracks and event annotations (CSV-style `.viratdata` files) |

**Contents:** VIRAT Ground 2.0 — 329 surveillance videos from stationary ground
cameras at height, across 11 different scenes.

**Why it matters:** stationary outdoor footage with object tracks makes it the primary
basis for the labelled query set behind SM-1 (≥ 85 % recall@5).

**Checklist**
- [ ] Account registered
- [ ] Downloaded
- [ ] Extracted and verified
- [ ] Labelled query set built

---

## 5. SoccerNet

**Domain:** Sports · **Role:** PFM sports head · cross-domain transfer (SM-5)

| Field | Value |
|---|---|
| **Licence** | NDA + research-use conditions |
| **Size on disk** | Varies by task — features are far smaller than raw video |
| **Access** | **NDA form required.** Submit the form, receive a password by email, use it to extract the video files |
| **Download** | `pip install SoccerNet`, then download via the Python package |
| **Source** | https://www.soccer-net.org/data |
| **Approval time** | Short — the password arrives by email (**check spam**) |
| **Annotation format** | JSON action-spotting labels with timestamps |

**Contents:** 500 + 50 broadcast soccer matches, `.mkv`, 25 fps, 720p or 224p, with
densely timestamped events (goals, fouls, cards).

**⚠ Submit this one first** — it is the only dataset with any waiting period.

**Tip:** pre-extracted **video features at 2 fps** are also offered. These are far
smaller than the raw broadcast video and may be sufficient for the temporal model,
which would save a large amount of disk space and download time. Evaluate before
committing to the full video download.

**Checklist**
- [ ] NDA form submitted
- [ ] Password received
- [ ] Downloaded
- [ ] Extracted and verified
- [ ] Loader written

---

## Disk space planning

Rough total for full raw downloads: **250 GB+**. Before starting, confirm available
space on both machines and decide where the data lives (external drive, shared
storage, or per-machine). Consider whether pre-extracted features are sufficient for
SoccerNet, and whether a subset of UCF-Crime is enough for early development.

## Open questions

- [ ] Confirm exact size of AI City Challenge Track 2.
- [ ] Decide: SoccerNet raw video, or 2 fps pre-extracted features?
- [ ] Decide where the datasets are stored, and whether both of us keep a local copy.
- [ ] Confirm UCF-Crime download size against available disk.