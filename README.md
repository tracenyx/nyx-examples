# Nyx Policy Examples

Copy-paste network policy examples for common Kubernetes security
scenarios — enforced at the kernel by Nyx (eBPF on Linux, WFP on Windows).

Each example is a standalone, validated policy you can adapt to your own
namespaces and workloads.

## Categories

### Basics
- `basics/default-deny-cross-namespace.yaml` — zero-trust baseline;
  deny cross-namespace, allow same-namespace
- `basics/allow-frontend-to-api-gateway.yaml` — restore a single
  legitimate cross-namespace path

### Egress control
- `egress/allow-fqdn-egress.yaml` — allow egress to specific hostnames
  only (FQDN-based, kernel SNI enforcement)
- `egress/fqdn-default-deny-egress.yaml` — allow one approved hostname
  and deny all other egress in the same policy (self-contained lockdown)

### Workload isolation
- `isolation/payments-ingress-allowlist.yaml` — restrict a sensitive
  service to a single allowed caller (PCI-style hardening)
- `isolation/intra-namespace-deny.yaml` — prevent lateral movement
  between services in the same namespace

### Platform policies
- `platform/cluster-baseline.yaml` — cluster-wide platform guardrail
  (NyxClusterNetworkPolicy, tier: platform) that no app team can override

### Windows
- `windows/windows-wfp-policy.yaml` — the same policy model enforced on
  Windows Server via WFP, demonstrating Linux/Windows parity

## How policies are evaluated

- Rules within a policy are evaluated top-down, first match wins.
- Across policies, lower priority number is evaluated first.
- Priority bands: platform-override (0–99), namespace (100–9,999),
  platform-baseline (10,000–19,999), workload (20,000–99,999).

## Try it end to end

For a full guided walkthrough using a sample application on both Linux
and Windows, see the tutorial:
**https://github.com/tracenyx/nyx-demo**

## Documentation

Full documentation: **https://docs.tracenyx.ai**

## Get Nyx

Free Scout tier — three namespaces, no credit card:
**https://tracenyx.ai**
