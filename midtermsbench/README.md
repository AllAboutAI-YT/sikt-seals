# MidtermsBench v1 seals

Fingerprints of Sikt Intelligence's 2026 US midterms benchmark: the pre-registration (event list, scoring plan and
amendments), the scoring code, and every round's forecasts, published before the results.

- `<day>.<n>.json`: sha256 of each file, plus per round a sha256 over the listing of every forecast session file.
  Only hashes; the files are revealed with the results.
- `<day>.<n>.tsr`: an RFC 3161 timestamp token from [FreeTSA](https://freetsa.org) for the json file.

Verify: `openssl ts -verify -data <day>.<n>.json -in <day>.<n>.tsr -CAfile cacert.pem -untrusted tsa.crt`.
The git history is a further timestamp.
