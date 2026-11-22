# CCSA108: HTTPS Inspection (Check Point R82)

# CheckPoint_CCSA_HTTPS_Inspection

Practical assignment documenting the planning, configuration, policy design, verification, and review of HTTPS Inspection on a Check Point R82 Security Gateway.

## Project overview

This repository contains the submitted assignment and supporting notes/evidence for the CCSA108 HTTPS Inspection practical.

### Objectives

- Plan a safe outbound HTTPS Inspection deployment.
- Enable HTTPS Inspection and review the deployment mode.
- Create outbound HTTPS Inspection rules, including trusted-site bypass handling.
- Publish/install the policy and document verification constraints.
- Review HTTPS Inspection global settings.
- Explain the difference between outbound and inbound HTTPS Inspection.

## Lab environment and constraints

- **Platform:** Check Point SmartConsole
- **Gateway version:** R82
- **Gateway hosting:** Cloud-hosted Security Gateway
- **Management access:** Remote access through VPN
- **Observed access limitation:** The assignment records that the host at `192.168.11.201` did not respond to ping. The report attributes this to limitations in accessing the cloud-hosted gateway environment. This is recorded as a verification limitation, not proof that HTTPS Inspection itself failed.

## Repository structure

```text
CCSA108-HTTPS-Inspection/
├── README.md
├── .gitignore
├── docs/
│   ├── CCSA108-HTTPS-Inspection-Assignment.pdf
│   └── implementation-notes.md
└── evidence/
    └── README.md
```

## Practical tasks

| Task | Scope | Evidence/status in submitted report |
|---|---|---|
| 1. Plan the deployment | Trusted CA certificate distribution; gradual deployment | Planning notes reference the R82 Release Notes, page 14 |
| 2. Enable HTTPS Inspection | Configure outbound inspection and select deployment mode | SmartConsole screenshot included in the assignment PDF |
| 3. Create the HTTPS Inspection policy | Configure bypass and inspect rules | Policy screenshot included in the assignment PDF |
| 4. Publish, install and verify | Publish/install policy and test connectivity | Ping test is documented; target host did not respond |
| 5. Review global settings | Fail Mode, Categorization Mode and Server Validations | Screenshots included in the assignment PDF |

## Key technical points

### Outbound HTTPS Inspection

The gateway intercepts an internal client's HTTPS session and establishes two separate TLS connections:

1. **Client-to-gateway:** The gateway presents a substitute certificate signed by its outbound inspection CA. The client must trust that CA.
2. **Gateway-to-server:** The gateway establishes a separate TLS connection to the external server using the server's genuine certificate. The gateway decrypts and inspects traffic, then re-encrypts and forwards it.

### Certificate trust

The outbound inspection CA certificate must be installed in the clients' Trusted Root Certification Authorities store. Without client trust, browsers and applications may report certificate warnings.

### Bypass policy

Trusted sensitive services, particularly online banking and financial services, should be considered for bypass. Certificate pinning and mutual TLS can also cause compatibility problems with HTTPS Inspection. A bypass rule should be ordered above a general inspection rule when that is the intended policy behavior.

### Gradual deployment

The assignment describes using Learning Mode with Gradual and Smart Deployment, beginning with a limited percentage/subset of traffic and observing connectivity, application compatibility, and gateway performance before expanding inspection.

### Global settings reviewed

- **Fail Mode:** Determines whether traffic is allowed without inspection (Fail-Open) or blocked (Fail-Close) when inspection cannot be performed.
- **Categorization Mode:** Determines how website categorization is applied while making HTTPS Inspection decisions.
- **Server Validations:** Controls certificate validation checks for external servers.

## Theory section

The submitted assignment includes answers to:
- Outbound HTTPS Inspection purpose.
- Certificate and private-key requirements for inbound HTTPS Inspection.
- Static NAT destination matching in an HTTPS Inspection rule.
- Recommended gradual rollout.
- The two TLS connections in outbound inspection.
- Outbound versus inbound inspection.
- Client trust and trusted-site bypass.
- HTTPS Inspection global settings.
- Troubleshooting certificate warnings and privacy concerns.

Refer to `docs/CCSA108-HTTPS-Inspection-Assignment.pdf` for the complete submitted answers and original screenshots.

## Important limitations and responsible use

- This repository documents a training lab and its observed evidence. It does not claim a production deployment.
- The assignment reports a failed ping to `192.168.11.201` and identifies cloud-hosting access limitations. Additional verification (for example, browser certificate inspection, HTTPS access tests, gateway logs, and policy installation status) should be performed where access is available.
- Do not commit private keys, exported CA private material, passwords, VPN profiles, customer data, or unredacted secrets.
- Only inspect traffic and deploy certificates on systems for which you have explicit authorization.

## Reference

- Check Point R82 Release Notes, dated 14 September 2026, page 14 (HTTPS Inspection), as cited in the assignment.

## Author

Adio Kabiru
