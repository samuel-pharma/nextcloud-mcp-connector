# Third party licences

The connector itself is AGPL-3.0-or-later (see [LICENSE](LICENSE)). The
container image and standalone installs carry the following direct runtime
dependencies; the licence names are the `License` metadata of the exact
versions locked in `uv.lock`, and the pin policy behind them is
`docs/dependency-audit.md`.

## Runtime

| Package | Licence |
|---|---|
| mcp (official MCP SDK, with httpx2 as its internal client) | MIT (httpx2: BSD-3-Clause) |
| cryptography | Apache-2.0 OR BSD-3-Clause |
| PyJWT | MIT |
| httpx | BSD-3-Clause |
| lxml | BSD-3-Clause |
| icalendar | BSD-2-Clause |
| vobject | Apache-2.0 |
| pydantic | MIT |
| tzdata | Apache-2.0 (IANA time zone data) |

## The `documents` extra (always in the ExApp image)

| Package | Licence |
|---|---|
| python-docx | MIT |
| openpyxl | MIT |
| python-pptx (pulls Pillow and XlsxWriter) | MIT (Pillow: MIT-CMU, XlsxWriter: BSD-2-Clause) |
| pypdf | BSD-3-Clause |

## Base image

The container builds on `python:3.13-slim` (Debian packages under their
respective licences, CPython under the PSF License).
