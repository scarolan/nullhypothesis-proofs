# NullHypothesis Proof Checkpoints

Cryptographic proof-of-detection timestamps for [NullHypothesis.ai](https://nullhypothesis.ai).

## Purpose

This repository provides tamper-proof evidence of when papers were flagged by our scientific integrity scanner. Each checkpoint contains SHA256 hashes of our detection database, allowing independent verification that predictions existed before retractions occurred.

## Checkpoint Format

Each daily checkpoint (`checkpoints/YYYY-MM-DD.json`) contains:

```json
{
  "timestamp": "ISO 8601 UTC timestamp",
  "fingerprint_version": "vX.Y.Z",
  "fingerprint_checksum": "SHA256 of detection patterns",
  "predictions_checksum": "SHA256 of predictions database",
  "pmc_findings_checksum": "SHA256 of raw PMC findings",
  "stats": {
    "total_predictions": 1234,
    "watching": 1100,
    "retracted": 134
  }
}
```

## Verification

To verify a checkpoint:

1. The `fingerprint_checksum` proves which detection patterns were active
2. The `predictions_checksum` proves the database state at checkpoint time
3. GitHub's commit timestamp provides external anchoring we cannot forge

When a paper is retracted, compare:
- Our `predicted_at` timestamp in the database
- The checkpoint commit date proving that prediction existed
- The retraction date from CrossRef/OpenAlex

## "Called It" Claims

We only claim "Called It" when:
1. Paper was in our predictions database BEFORE retraction
2. Checkpoint commit predates the retraction
3. Both timestamps are independently verifiable

## Contact

Questions about methodology: p@nullhypothesis.ai
