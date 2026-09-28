# Sikt Intelligence: capture seals

Public fingerprints of Sikt Intelligence's forecasting archive. Each day, everything the capture service recorded
(search result lists, web pages, market states, question registrations) is sealed: every record is hashed, and the
hashes are combined into one Merkle root. This repository publishes, per sealed batch:

- `fingerprints/<day>.<batch>.json`: the day, record range and count, the Merkle root and the sha256 of the full seal
  file;
- `fingerprints/<day>.<batch>.json.ots`: an [OpenTimestamps](https://opentimestamps.org) proof (anchored in Bitcoin)
  for the seal file;
- `fingerprints/<day>.<batch>.tsr`: an RFC 3161 timestamp token from [FreeTSA](https://freetsa.org) for the seal file.

Only hashes are published: no article text, URLs or question list. The git history is a further timestamp.

**What this proves.** When we later reveal a record (for example "these were the top news results for a question on
this date") together with the seal file, anyone can check that the record's hash is in the Merkle root, that the seal
file matches the published sha256, and that both timestamps predate the event the record is about. So the archive
cannot have been assembled or edited after the fact.

Verify a timestamp: `ots verify fingerprints/<day>.<batch>.json.ots -f <seal file>` and
`openssl ts -verify -data <seal file> -in fingerprints/<day>.<batch>.tsr -CAfile cacert.pem -untrusted tsa.crt`.
