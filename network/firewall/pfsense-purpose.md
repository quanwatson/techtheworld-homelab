# pfSense Purpose and Role

## Objective

pfSense will act as a boundary firewall between the existing home network
and a dedicated homelab network.

It will NOT replace the home router.

## Responsibilities

- Provide routing and NAT for the homelab subnet
- Enforce firewall rules between zones
- Offer a platform for learning firewall concepts
- Support services such as VPN and VLANs in the future

## Non-Goals

- Managing household Wi-Fi
- Replacing the Deco mesh system
- Acting as the primary internet gateway for the home

## Design Principle

Isolation before optimization.
