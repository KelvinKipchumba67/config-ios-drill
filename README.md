# IOS Drill

A simulated Cisco IOS command-line terminal for CCNA config-mode practice. Single HTML file, no dependencies, works offline in any browser.

## What it does

- **Real mode transitions** - moves through the actual IOS mode hierarchy as you type:
  `Router>` (user exec) → `Router#` (privileged exec) → `Router(config)#` (global config) → `Router(config-if)#` / `Router(config-line)#` / `Router(config-router)#`
- **Command abbreviation** - works the way real IOS does: `conf t`, `int g0/0`, `en`, `wr` all resolve correctly
- **Authentic error messages** - an invalid command in the wrong mode returns `% Invalid input detected at '^' marker.`; a command missing required arguments returns `% Incomplete command.`
- **Enable password gate** - once you set an `enable secret` or `enable password`, typing `enable` afterward actually prompts for it (input masks like a password field) before dropping you into privileged exec
- **Command history** - Arrow Up/Down cycles through previously entered commands, like a real terminal
- **Live `show` commands** - `show running-config`, `show ip interface brief`, `show ip route`, `show interfaces`, and `show version` all reflect the current simulated device state
- **8-task checklist** in the sidebar tracks real CCNA-style objectives and checks off automatically as your configuration satisfies them
- **Quick reference panel** for when you blank on syntax mid-drill

## Supported commands

**User exec**
- `enable`
- `ping <ip>`
- `show version`

**Privileged exec**
- `configure terminal`
- `show running-config`
- `show ip interface brief`
- `show ip route`
- `show interfaces`
- `copy running-config startup-config` / `write memory` / `write` / `wr`
- `reload` (simulated message only, no actual reset)
- `disable`

**Global config**
- `hostname <name>`
- `interface <name>` (accepts short forms: `g0/0`, `gi0/0`, `fa0/1`, `s0/0/0`, `lo0`, `vlan1`)
- `line console 0` / `line vty 0 4`
- `router ospf <process-id>`
- `ip route <network> <mask> <next-hop>`
- `enable secret <password>` / `enable password <password>`
- `service password-encryption`
- `no ip domain-lookup`
- `ip domain-name <name>`
- `username <name> password <password>`
- `banner motd <delimiter>text<delimiter>`

**Interface config**
- `ip address <ip> <mask>`
- `no shutdown` / `shutdown`
- `description <text>`
- `switchport mode access|trunk`
- `duplex` / `speed` (accepted, no-op)

**Line config**
- `password <password>`
- `login` / `login local`
- `transport input ssh|telnet|all|none`
- `exec-timeout` (accepted, no-op)

**Router config (OSPF)**
- `network <network> <wildcard> area <n>`
- `router-id <ip>`

**Universal**
- `exit`, `end`, `?`

## How to use it

1. Open `index.html` in any browser - no server or install needed.
2. Type `enable` to move into privileged exec, then `configure terminal` to start configuring.
3. Work through the task checklist on the right, or freeform practice any topic you're studying (interfaces, static routing, OSPF, line security).
4. Use `show running-config` at any point in privileged exec to see the full config your commands have built.
5. **Reset device** in the header wipes all configuration and starts over - use it between drill sessions or scenarios.

## Notes on realism / limitations

- This is a single simulated device - there's no second router or switch to actually route packets to, so `ping` always simulates success and OSPF has no neighbors to form adjacencies with. It's built for practicing **syntax and configuration logic**, not multi-device behavior.
- `show ip route` displays directly connected and static routes only; OSPF-learned routes aren't simulated since there's nothing on the other end to learn from.
- Passwords are stored and displayed in the running-config as you typed them (the `service password-encryption` flag is tracked but doesn't produce a real type-7 encoded string).
- The enable-password prompt accepts one attempt before failing back to user exec - real IOS retries three times before dropping the connection.
- Layout and configuration aren't saved between browser sessions - if you close the tab, the simulated device resets.

## Possible next additions

- A second simulated device to practice full point-to-point topologies (ping that actually succeeds/fails based on reachability)
- VLAN database commands and inter-VLAN routing
- ACL configuration and `show access-lists`
- NAT/PAT configuration
- DHCP pool configuration
- Scenario picker with multiple task sets instead of one fixed checklist

---
