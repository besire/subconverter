# Add Mihomo SSH Output Support

## Goal

Support SSH outbound nodes when generating Mihomo-compatible Clash YAML output, so an input subscription/configuration that contains an SSH proxy can preserve it instead of dropping it during conversion.

## Confirmed Facts

- The repository currently has no `ProxyType::SSH` and no SSH parser/output branch.
- Mihomo output is generated through the existing Clash YAML path in `proxyToClash`.
- Clash YAML input parsing is handled by `explodeClash`, which already supports most Mihomo-style proxy node fields.
- Mihomo's SSH proxy schema uses `type: ssh` with common fields such as `server`, `port`, `username`, `password`, `private-key`, `private-key-passphrase`, `host-key`, and `host-key-algorithms`.

## Requirements

- Add an internal SSH proxy type that can be matched, labeled, and carried through node manipulation like other proxy types.
- Parse Mihomo/Clash YAML SSH nodes from `proxies` or `Proxy` sections.
- Generate Mihomo-compatible SSH YAML nodes from internal SSH proxies.
- Preserve SSH authentication fields:
  - `username`
  - `password`
  - `private-key`
  - `private-key-passphrase`
  - `host-key`
  - `host-key-algorithms`
- Preserve `dialer-proxy` through the existing underlying proxy mechanism.
- Do not add SSH output to unrelated target formats in this task.
- Do not change behavior for existing proxy types.

## Acceptance Criteria

- [ ] A Clash/Mihomo YAML input containing `type: ssh` is parsed into a non-unknown node.
- [ ] Mihomo/Clash output includes an SSH node with `type: ssh`, server, port, username, and authentication fields.
- [ ] Optional SSH list fields `host-key` and `host-key-algorithms` round-trip through YAML parsing and output.
- [ ] Existing non-SSH Clash/Mihomo output behavior remains unchanged.
- [ ] The project builds or the touched files pass the repository's available compile checks.

## Notes

- Source for Mihomo SSH fields: https://wiki.metacubex.one/en/config/proxies/ssh/
