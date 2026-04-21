# SNMP Lab Documentation

End-to-end network management lab covering SNMP operations, monitoring workflows, and management-plane security hardening on Cisco IOS.

This repository documents a practical implementation across two phases:
- Phase 1: SNMPv1/v2c monitoring, trap handling, MIB walks, and packet inspection
- Phase 2: SNMPv3 secure management (authPriv), access-control validation, and encrypted traffic analysis

## Project Scope

- Build a working manager-agent topology in GNS3
- Configure SNMP manager and SNMP agent connectivity
- Validate asynchronous trap delivery and MIB retrieval
- Compare SNMPv1 and SNMPv2c operational behavior
- Harden management with SNMPv3 users, groups, and views
- Verify encrypted/decrypted SNMPv3 packets in Wireshark

## Lab Stack

- Cisco IOS router (R1) in GNS3
- SnmpB (manager, MIB browser, trap viewer)
- Wireshark + WinPcap (traffic capture and protocol analysis)
- Windows loopback adapter for host-router management path

## Topology and Addressing

- Manager host (Loop1): `172.16.0.2/24`
- Router R1 `f0/0`: `172.16.0.1/24`
- Router R1 `f1/0`: used for LinkUp/LinkDown trap testing

## Documentation

Main technical documentation is available in:
- [Lab_Documentation.tex](Lab_Documentation.tex)

If you want a PDF output:
1. Open `Lab_Documentation.tex` in a LaTeX editor (or use `pdflatex`)
2. Compile twice to ensure table-of-contents and references are resolved

## Key Implementation Highlights

### Phase 1: SNMPv1/v2c Operations
- Community-based access configured with ACL restriction
- Trap receiver configured on manager host
- Validation of `coldStart`, `linkUp`, and `linkDown` traps
- MIB walk over `mib-2.system`
- SNMPv1 vs SNMPv2c packet pattern comparison (`GetNext` vs `GetBulk`)

### Phase 2: SNMPv3 Security Hardening
- Engine ID configuration on Cisco IOS
- View/group/user model for role-based authorization
- `authPriv` security level with SHA authentication and DES privacy
- Successful write operations with privileged user
- Write denial with read-only user
- Wireshark decryption after SNMP user table provisioning

## Security Notes

- SNMPv1/v2c community strings are plaintext and should not be used on untrusted networks.
- SNMPv3 with `authPriv` should be the baseline for production-grade deployments.
- Access should be limited using ACLs, views, and least-privilege user/group design.

## Next Improvements

- Upgrade privacy protocol from DES to AES where supported
- Add redundant trap destinations
- Expand monitoring scope to interface, IP, and performance MIBs
- Integrate telemetry into a dashboard/time-series stack