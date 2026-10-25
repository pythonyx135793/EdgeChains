# Qdrant REST client validation

Source: `2900660409b5c1e5098528d14d07a4e2966abacb`, based on upstream `0467bbc0fa6971e0f5e542648ebff167f8053586`.

[Short demo](qdrant-demo-id-fix.webm) · [Completed demo screenshot](demo-complete-id-fix.png) · [File hashes and results](MANIFEST.json)

The video runs the committed example through the built SDK export against a real local Qdrant 1.20.0 server. It creates a collection, inserts three synthetic document vectors, retrieves the two matching documents with a payload filter, updates payload, deletes a point and removes its collection. The browser is Chrome 155 in headless mode. No embedding service is called.

On Windows with Node 24.19.0:

- 64 loopback HTTP request/error tests passed.
- 14 actual Qdrant service tests passed through the built package export; zero skipped.
- The SDK build, standalone strict type check of both new test files and formatting check passed.
- The full repository test command exits 1: its three existing failed assertions and twelve existing file-load failures remain. The original-source report is included. The older baseline comparison records a missing optional Playwright-browser path difference caused by the isolated test environment; it does not establish byte-for-byte error equality.

The ID control records six invalid-ID HTTP requests from the earlier implementation versus six local rejections and zero requests after correction. This control is separate from the actual-service tests.

The source manifest binds the six submitted files to their Git blobs and SHA-256 values. `full-tests-id-fix.json` is the current raw test report; `COMMANDS-id-fix.json` records command exits. Empty build/type logs mean those commands completed without diagnostics, as recorded in the command report. The disposable server was stopped and its listening port checked after the demo.

To reproduce the feature tests, follow the example and test commands in the SDK README, build first, and explicitly set `QDRANT_URL` to a disposable server. Without that variable the service tests are intentionally skipped; a skipped service run is not equivalent to the results here.
