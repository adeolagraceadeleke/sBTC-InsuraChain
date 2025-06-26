
# sBTC-InsuraChain - Decentralized Insurance Smart Contract

This smart contract provides a decentralized insurance management system on the Stacks blockchain using Clarity. It allows insurers to issue policies, collect premiums, assess risk, and handle claims in a secure and automated manner.

---

## 🚀 Features

* **Policy Management**: Initiate, activate, renew, or cancel insurance policies.
* **Premium Handling**: Secure transfer and tracking of premium payments.
* **Claim Lifecycle**: Submit, approve, and payout insurance claims.
* **Risk Assessment**: Insurers can assess and update policyholder risk profiles.
* **Transparency & Logs**: Blockchain-based event logging for all critical actions.
* **Configurable Constants**: Grace period, max coverage, and more are defined as constants.

---

## 🛠️ Setup & Deployment

### Requirements

* [Clarity Language](https://docs.stacks.co/write-smart-contracts)
* [Clarinet](https://docs.stacks.co/understand-stacks/clarinet)
* Stacks blockchain development environment

### Constants

```clojure
(define-constant grace-period u1000)
(define-constant max-coverage u1000000)
```

### Maps

* `insurance-policies`
* `insurance-claims`
* `policy-history`
* `risk-scores`

---

## 🔧 Core Functions

### 1. `initiate-policy`

```clojure
(initiate-policy (new-insurer principal) (new-insured-party principal) (premium-amount uint) (coverage-amount uint))
```

Creates a new insurance policy for a user.

---

### 2. `submit-premium`

```clojure
(submit-premium (insured principal))
```

Activates or renews a policy after premium payment.

---

### 3. `submit-claim`

```clojure
(submit-claim (insured principal) (claim-amount uint))
```

Files a claim against an active policy.

---

### 4. `approve-claim`

```clojure
(approve-claim (insured principal))
```

Approves a pending claim request.

---

### 5. `release-payout`

```clojure
(release-payout (insured principal))
```

Releases funds to the insured party after claim approval.

---

### 6. `cancel-policy`

```clojure
(cancel-policy (insured principal))
```

Cancels an active policy and calculates a proportional refund.

---

### 7. `update-risk-assessment`

```clojure
(update-risk-assessment (insured principal) (new-risk-score uint))
```

Allows insurers to update the risk score of a policyholder, dynamically adjusting premiums.

---

### 8. `adjust-premium-by-risk` *(Private Function)*

```clojure
(adjust-premium-by-risk (risk-score uint) (current-premium uint))
```

Adjusts premium based on normalized risk factor (risk score 1–100).

---

## 🔒 Access Control & Validations

* **Initiation Restrictions**: Policy initiator must not be the insured.
* **Premium Submission**: Only valid if policy is inactive or expired.
* **Claim Limitations**: Claims cannot exceed coverage; policies must be active.
* **Cancellation**: Can only be done by the insurer or the insured.
* **Risk Assessment**: Only insurers can update risk scores.

---

## 🧾 Event Logs

Events are printed using the `print` function for traceability:

* `insurance-policy-created`
* `premium-paid`
* `claim-filed`
* `claim-approved`
* `payout-released`
* `policy-cancelled`
* `risk-assessment-updated`

---

## 📈 Example Use Flow

1. Insurer calls `initiate-policy`.
2. Insured party calls `submit-premium` to activate.
3. In case of incident, insured submits a claim via `submit-claim`.
4. Insurer approves via `approve-claim`.
5. Insured or insurer executes `release-payout`.
6. Policy can be updated or canceled at any time.

---

## 🧪 Testing

Use Clarinet to write unit and integration tests:

```bash
clarinet test
```

---

## 📝 License

This contract is open-source and intended for educational or experimental use. Conduct proper audits before using in production environments.
