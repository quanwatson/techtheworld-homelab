# pfSense Rollback Plan

## Risk

Improper configuration could disrupt homelab access.

## Rollback Procedure

1. Disconnect pfSense WAN cable
2. Power off pfSense device
3. Reconnect homelab devices directly to Deco if needed

## Recovery Guarantee

Home network remains unaffected because:
- Deco remains the primary router
- No changes are made to Deco configuration
- pfSense is downstream only
