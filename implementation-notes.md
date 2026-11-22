# Implementation notes

## Task 1: Deployment plan

The report identifies two deployment considerations:

1. **Trusted CA certificate deployment:** Export the outbound inspection CA certificate from the Security Gateway and install it in the internal test host's Trusted Root Certification Authorities store.
2. **Gradual and Smart Deployment:** Start by inspecting a limited percentage/subset of traffic. Use Network Learning to observe application/network behavior and Performance Prediction to estimate the impact of full inspection. Expand only after reviewing connectivity, compatibility, and performance.

The report cites the Check Point R82 Release Notes, page 14.

## Task 2: Enable HTTPS Inspection

The submitted SmartConsole screenshot records the HTTPS Inspection configuration workflow and the selected deployment approach. See the original evidence in the assignment PDF, page 2.

## Task 3: HTTPS Inspection policy

The submitted policy screenshot shows an outbound policy with:
- A trusted-site bypass rule for selected financial/health-related categories.
- A general outbound inspection rule for internal LAN traffic.

Review the actual rule order and scope in the SmartConsole environment before applying any policy changes.

## Task 4: Publish, install and verify

The report includes a ping test to `192.168.11.201`, which timed out. The report states that the host was not responding because the Security Gateway was cloud-hosted and access was limited.

This test alone does not establish whether HTTPS Inspection is functioning. If lab access becomes available, supplement it with:
- Policy installation status in SmartConsole.
- HTTPS browsing tests from an authorized client.
- Certificate-chain inspection in the browser.
- Gateway logs showing the HTTPS Inspection action.
- A controlled test of a bypassed site and an inspected site.

## Task 5: Global settings

The submitted screenshots review:
- **Fail Mode:** Fail-Open versus Fail-Close for server-side and client-side inspection failures.
- **Categorization Mode:** Background/allow while categorization completes versus hold/block until categorization completes.
- **Server Validations:** Rejection conditions for untrusted, revoked, and expired server certificates, plus the configured action for validation errors.

Consult the screenshots in the assignment PDF, pages 4-5, for the exact selections visible in the lab.

## Theory answers

The complete theory answers are retained in the submitted assignment PDF, pages 5-7. This notes file intentionally summarizes the topics rather than replacing the original submission.
