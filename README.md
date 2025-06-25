

# sBTC-WebShield - Anti-Phishing Smart Contract

A secure, decentralized smart contract system on the Stacks blockchain designed to combat phishing threats and protect users from malicious websites. This system leverages **community-driven threat detection**, **proof-backed reporting**, and **trust-based sentinel validation**, providing an auditable, on-chain registry of suspicious domains and safe site endorsements.

---

## 🚀 Features

### ✅ Site Registration & Verification

* **Site owners** can register their web identifiers by staking collateral.
* Each site is associated with a `security_endorsement` and metadata like `authentication_level`, `threat_metric`, and `locked_assets`.

### 🔍 Threat Detection & Alerts

* **Sentinels** can submit phishing alerts by attaching `proof_documentation` and a `threat_magnitude`.
* Reports are stored in the `malicious_site_registry` with a pending confirmation state.

### 📈 Sentinel Reputation System

* Sentinels build **credibility** over time through verified threat submissions.
* Credibility scores impact the ability to submit alerts.
* Every submission and validation updates sentinel metrics stored in `sentinel_performance_log` and `sentinel_registry`.

### ⚖️ Threat Validation

* Sentinels validate threat reports, affecting site `threat_metric`.
* Positive validations increase a site's risk score; invalidations reduce it.

### 🔐 Collateralization

* Both site owners and sentinels must stake STX to participate.
* Ensures skin-in-the-game and discourages spam/malicious behavior.

### 🛑 Emergency Controls

* `system_controller` can:

  * Pause/unpause the contract globally.
  * Adjust protection intensity (`protection_intensity`).
  * Transfer system control (`reassign_system_control`).

---

## 🗂️ Data Models

### `registered_sites`

Tracks verified websites with:

* `site_proprietor`
* `authentication_level`
* `threat_metric`
* `security_endorsement`

### `malicious_site_registry`

Stores flagged phishing domains:

* `proof_documentation`
* `threat_magnitude`
* `confirmation_state`

### `sentinel_registry` & `sentinel_performance_log`

Monitor sentinel activity:

* `credibility_score`
* `verified_submissions`
* `reserved_amount`

---

## ⚙️ Key Functions

### 🛠 Admin Functions

| Function                  | Description                                        |
| ------------------------- | -------------------------------------------------- |
| `initialize_system`       | Sets initial controller and resets state.          |
| `modify_protection_level` | Adjusts global protection/collateral requirements. |
| `toggle_system_state`     | Pauses/resumes all major operations.               |
| `reassign_system_control` | Transfers control to a new principal.              |

### 🧾 Site Functions

| Function               | Description                                    |
| ---------------------- | ---------------------------------------------- |
| `register_secure_site` | Registers a new secure site by the controller. |
| `fetch_site_status`    | Returns site metadata.                         |
| `check_threat_status`  | Returns if a site is flagged as phishing.      |

### 🚨 Sentinel Functions

| Function                 | Description                               |
| ------------------------ | ----------------------------------------- |
| `enlist_sentinel`        | Registers a new sentinel with collateral. |
| `submit_threat_alert`    | Submits phishing alert with proof.        |
| `validate_threat_report` | Confirms or rejects existing alert.       |
| `fetch_sentinel_rating`  | Returns sentinel’s credibility score.     |

---

## 📌 Security & Validation

The contract ensures:

* Only the **controller** can register sites.
* Stringently **validates input strings** (e.g., web identifiers, endorsements, proofs).
* Enforces **collateral requirements** to discourage abuse.
* Applies **rate-limiting** using `INACTIVITY_WINDOW` to prevent spam submissions.

---

## 🧪 Error Codes

| Code        | Meaning                                                      |
| ----------- | ------------------------------------------------------------ |
| `u100`      | Access Forbidden                                             |
| `u101`      | Duplicate Entry                                              |
| `u102`      | Entry Missing                                                |
| `u103`      | Operation Blocked                                            |
| `u104`      | Missing Collateral                                           |
| `u105`      | Submission too soon                                          |
| `u106`      | Protection Limit Breach                                      |
| `u107`      | Temporal Logic Error                                         |
| `u400–u405` | Input validation failures (web ID, endorsement, proof, etc.) |

---

## 🔐 Constants

| Constant                      | Value            | Description                       |
| ----------------------------- | ---------------- | --------------------------------- |
| `INACTIVITY_WINDOW`           | `86400`          | Time between submissions (24h)    |
| `BASE_COLLATERAL_REQUIREMENT` | `1_000_000 µSTX` | Default staking amount            |
| `TRUSTWORTHINESS_BASELINE`    | `50`             | Minimum credibility to report     |
| `EVIDENCE_STRING_LIMIT`       | `500`            | Max length of proof documentation |

---

## 🧑‍💼 Governance Model

The contract is governed by a **system controller** with exclusive rights to:

* Onboard secure sites
* Adjust thresholds
* Delegate control

In the future, this role can be transitioned to a DAO or voting mechanism.

---

## 📬 Example Usage

### Registering a Secure Site:

```clojure
(register_secure_site "bank-secure" "ISO-certified 2024")
```

### Submitting a Phishing Alert:

```clojure
(submit_threat_alert "fake-exchange" "Found phishing login flow" u90)
```

### Validating Threat:

```clojure
(validate_threat_report "fake-exchange" true)
```

---

## 🧩 Future Improvements

* Voting-based confirmation system for flagged threats
* Escrowed collateral slashing for malicious submissions
* Integration with off-chain monitoring/oracle feeds
* DAO-managed control of `system_controller`

---

## 📄 License

MIT — Free for public use, modification, and research.

