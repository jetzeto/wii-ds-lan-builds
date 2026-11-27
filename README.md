# Private Wii–DS LAN builds for Windows

Personal distribution of the paired experimental Dolphin and melonDS Windows
x64 builds. This repository and its release assets are private.

## Downloads

Open the [Windows release](https://github.com/jetzeto/wii-ds-lan-builds/releases/tag/windows-lan-2026-11-27) and download:

- `Dolphin-LAN-IP-Settings-Windows-x64.zip`: Dolphin with persistent LAN peer IP
  settings under Settings → Wii.
- `melonDS-LAN-Windows-x64.zip`: melonDS with configurable LAN transport through
  the included `Launch-LAN.cmd`.
- `Windows-WiiDS-LAN-source-patches.zip`: matching source patches and build
  information. These are patches against the pinned upstream sources below.

The release includes SHA-256 checksums. Extract the emulator ZIPs into separate
folders and retain all DLLs, plugins and runtime data. No games, BIOS, firmware,
NAND dumps, saves, signing keys or personal emulator profiles are included.

## LAN setup

1. Open Dolphin.exe directly. Under Settings → Wii, enable Connect to melonDS
   and enter the IPv4 address of the phone or PC running melonDS. Leave the
   address field to save it. It applies at the next game launch.
2. On the melonDS PC, run Launch-LAN.cmd and enter the Dolphin PC's IPv4 address.
3. Allow both executables through the private-network firewall if required.
   The melonDS bridge listens on UDP ports 7065–7080. No internet relay or router
   port forwarding is needed.
4. Use the connection menus inside the games. Keep backups of in-game saves.

For same-PC mode, clear Dolphin's address field (or use 127.0.0.1), and launch
melonDS.exe directly without a configured WII_DS_PEER_IPV4 environment variable.
Saved Dolphin settings take precedence over the legacy environment variable.
These builds accept numeric IPv4 addresses, without DNS or IPv6 support.

## Sources and licensing

Both builds start from ATEMVEGETA's Wii–DS beta.4 sources:

- [Dolphin source](https://github.com/ATEMVEGETA/Dolphin/tree/wii-ds-link-v0.2.0-beta.4),
  revision 36c502b448d3d7ffa83398021b02bde49cee5e01. Apply
  `source-patches/Dolphin-lan.patch`, which includes the IP settings UI.
- [melonDS source](https://github.com/ATEMVEGETA/melonDS/tree/wii-ds-link-v0.2.0-beta.4).
  Apply `source-patches/melonDS-lan.patch`.

Build information and compiler/dependency versions are recorded in the two
BUILD-INFO JSON files. Follow each upstream source tree's build instructions;
Dolphin requires its pinned submodules. Runtime ZIPs include the original
project and dependency license notices. Dolphin is GPL-2.0-or-later and melonDS
is GPL-3.0-or-later; original notices and patch licensing are retained.

## Validation

The full Windows builds compiled, runtime dependency checks passed, and packaged
help/startup checks passed. Real socket tests covered HELLO/ACK, peer filtering,
STOP handling and invalid-address rejection on loopback and a same-PC LAN
interface. Dolphin's real INI tests verified save/reload and address precedence.
The user reported the experimental connectivity working. These automated checks
do not constitute comprehensive cross-device gameplay or save/transfer testing.
