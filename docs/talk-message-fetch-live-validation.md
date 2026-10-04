# Temporary live MCP validation

4 October 2026. MCP Connector 0.4.0, Nextcloud 34.0.4, Talk 24.0.5,
existing ExApp deployment, normal ChatGPT MCP tool with an existing non-admin
OAuth connection. Patch commit: 0e790ead69ccd1499b7efac53128add77e0c247e.

## Procedure and results

1. Verified installed talk.py and chatgpt.py SHA-256 values against the exact
   upstream v0.4.0 source. Saved both originals outside the connector container.
2. Verified the restoration copy operation with the original files. Prepared an
   independent host-side rollback script and a ten-minute fallback timer before
   applying the change; administrator SSH remained available independently of MCP.
3. Obtained only the byte count and SHA-256 of an existing, authorized message
   from Nextcloud as the comparison reference. No message was created for this trial.
4. Baseline normal MCP fetch returned 800 body bytes with truncated=true.
5. Replaced only the two changed modules with their exact commit contents and
   restarted only MCP Connector. Normal MCP fetch returned all 909 UTF-8 body
   bytes. The SHA-256 matched the independent reference, excluding the connector's
   author prefix. The truncation indicator was absent.
6. Normal talk_browse with limit=30 retained 800-byte previews and their truncation
   indicators. Its complete returned entry array was identical to the array read
   after rollback; comparisons were made in memory without publishing content.
7. A fabricated conversation token absent from this account's list returned the
   same denial before and during the patch. No permissions or credentials changed.
8. Executed rollback, restarted only MCP Connector, verified both original source
   hashes, and repeated normal MCP fetch. Its structured result exactly matched
   the baseline, including the original truncation. The fallback timer did not
   need to fire and was canceled; temporary deployment files were removed.
9. Unrelated application container start times were unchanged. Existing monitoring
   collectors remained alive and the host OOM count did not increase. Temporary
   SSH access was revoked, authentication refusal verified, and the private key deleted.

## Scope and limitations

This validates one actual message end-to-end through the normal OAuth/MCP path,
not just an internal function call. It does not establish a full permissions audit:
the negative case used a fabricated absent token, not a known private room of
another account. Existing synthetic permission/exclusion tests complement this
narrow live check. Oversized-body and Unicode boundary cases remain local tests;
the live message was not a 512 KiB boundary test.

An initial browse request with limit=100 was rejected by the connector schema's
maximum of 50 before execution; the actual comparison used limit=30 successfully.

No image build, complete integration suite, long-duration stability or upgrade
persistence was tested. After the reversible trial and a separate explicit authorization, the same patch
was reapplied, revalidated through the normal MCP tool with the same complete
response and unchanged preview, and retained on the deployment. Original files
and a manual rollback script were preserved; the automatic trial rollback was
canceled. A file-level
hotfix would need reapplication if its container is recreated; a released image
containing the reviewed source change is the maintainable deployment path.

No private message text, room or message identifiers, account names, credentials,
instance URLs, IP addresses or content hashes are included in this public report.
