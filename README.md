# World Buff Bots

An optional native module that schedules three Vanilla world-buff events for
eligible nearby characters in
[AzerothCore Playerbots Portable](https://github.com/Syntax555/mod-playerbots-portable).
The portable profile disables the simulator and uses native quest turn-ins by
default. This fork requires the assembly's matching Individual Progression and
core; no client addon is required.

## Install

Use the assembly's [Latest release and setup guide](https://github.com/Syntax555/mod-playerbots-portable#quick-start)
for a playable Windows server. The module is already included.
For native development, follow its
[build guide](https://github.com/Syntax555/mod-playerbots-portable/blob/main/docs/building.md)
and [dependency lock](https://github.com/Syntax555/mod-playerbots-portable/blob/main/versions.lock.json),
which selects a tested commit of this fork's `main` branch and matching dependencies.
Rebuild worldserver after native changes.

## Optional events

Set `WorldBuffBots.Enable = 1` to schedule events without a real quest turn-in.
Every recipient, human or bot, must be alive, outside GM mode, at most level 63
and in its own earned Vanilla era after the realm ceiling. The strict default
Individual Progression chain must be active; custom chains supply no buffs.

| Buff | Location | Additional requirement |
| --- | --- | --- |
| Warchief's Blessing | Orgrimmar; Crossroads 10 seconds later | Horde, Friendly or higher with Orgrimmar |
| Rallying Cry of the Dragonslayer | Stormwind | Native aura rules and lower-level scaling |
| Spirit of Zandalar | Stranglethorn Vale | Own Zul'Gurub entry tier, normally 3 |

Only characters present when an event fires receive its native aura. Each buff
has an independent 30–150 minute initial delay and a 90 ± 60 minute repeat timer.
Timers reset on startup or config reload. Native aura duration, immunity and
replacement remain active; real quest events are unchanged.

Announcements can use a generated display name; no character or quest turn-in
is created. Events award no quest credit, progression, items or money, and move
no characters. They do not supply TBC or Wrath buffs. See
[world buffs and limits](https://github.com/Syntax555/mod-playerbots-portable/blob/main/docs/world-buffs.md).

## Configuration

Edit `configs/modules/mod_world_buff_bots.conf` with the portable server stopped.
All keys are in [conf/mod_world_buff_bots.conf.dist](conf/mod_world_buff_bots.conf.dist).

| Setting | Portable default | Native template |
| --- | --- | --- |
| `WorldBuffBots.Enable` | `0` | `1` |
| `WorldBuffBots.BaseMinutes` / `VarianceMinutes` | `90` / `60` | Same |
| `WorldBuffBots.InitialMinMinutes` / `InitialMaxMinutes` | `30` / `150` | Same |
| `WorldBuffBots.Warchief.Enable`, `Dragonslayer.Enable`, `Zandalar.Enable` | `1` | Same |
| `WorldBuffBots.Warchief.IncludeCrossroads` | `1` | Same |
| `WorldBuffBots.Debug` | `0` | Same |

The three `*.Announcement` keys accept `{buff}` and display-only `{player}`
(or `%s`). Existing custom settings are preserved by portable updates; see
[configuration](https://github.com/Syntax555/mod-playerbots-portable/blob/main/docs/configuration.md).

## Source, contributions and license

Created by **Rockhopper1776**; maintained in
[Syntax555/mod-world-buff-bots](https://github.com/Syntax555/mod-world-buff-bots).
The [imported upstream README](https://github.com/Rockhopper1776/mod-world-buff-bots/blob/baae5656aa6a375e103bc83da8262f2061dbfcb6/README.md)
documents the original simulator; this fork's earned rules and portable defaults
above apply to the assembly.

Read [AGENTS.md](AGENTS.md) and the assembly's
[contribution workflow](https://github.com/Syntax555/mod-playerbots-portable/blob/main/CONTRIBUTING.md)
before changing this fork. Portable integration CI checks earned guards; native
builds and release integration run in the assembly.

**GNU Affero General Public License v3.0**, as declared by the upstream README.
See the [license text](https://www.gnu.org/licenses/agpl-3.0.html) and the assembly's
[third-party notices](https://github.com/Syntax555/mod-playerbots-portable/blob/main/THIRD_PARTY_NOTICES.md).
