# First Playable Roster

Working design for the opening tutorial slice. Names and numbers are tuning placeholders; the weapon identities and combat roles are the important first pass. Gameplay rules and definitions will be native C++ with GAS. No Blueprint-authored gameplay.

## Combat rules

- Guns are both firearms and the soldier's primary melee weapons. The defining move is a rifle-butt strike; firing remains useful for spacing and teaching the plague's resistance, but ammunition is scarce.
- Mutated villagers take 10% damage from bullets (90% reduction). Gun-butt impacts and radiation abilities use separate damage channels and are not reduced by bullet resistance.
- Initial GAS damage types: `Damage.Bullet`, `Damage.Bash`, `Damage.Radiation`. Enemy resistance belongs in damage calculation/effects, not per-weapon exceptions.
- Use `CombinatorCharge` as the spendable skill resource. Keep it distinct from `RadiationExposure`, the dangerous environmental buildup planned for later. The current prototype's generic `Radiation` attribute should be renamed/split before spells are implemented.
- Souls remain the level-up currency at lockers. Shops use recovered parts, so leveling and shopping do not compete for the same drop.

## Starter weapons

Baseline tuning uses the M1 Garand light bash as 100 impact, 100 speed, 100 stagger, 100 reach, and 100 stamina cost. These are relative tuning units, not final damage values.

| Weapon | Role | Impact | Speed | Stagger | Reach | Stamina |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| M1 Garand | Balanced service rifle; reliable light bash and committed heavy stock strike | 100 | 100 | 100 | 100 | 100 |
| M1 Carbine | Fast recovery and dodge follow-up; weaker poise damage | 75 | 125 | 65 | 90 | 70 |
| M1918A2 BAR | Heavy two-handed shove; excellent stagger, slow recovery | 155 | 70 | 160 | 105 | 140 |

The tutorial starts with the Garand. The Carbine and BAR are early finds, giving the player a fast and a heavy option without needing a weapon upgrade first.

## Rare weapons

Rare weapons have one clear combat modifier and remain historically recognizable. First candidates:

- **M1903 Springfield — Long Measure:** longest rifle reach; charged bash has high poise damage, with a slower wind-up.
- **Type 99 Arisaka — Salt Wind:** quick counter after a perfectly timed dodge; blunt rifle-stock attacks only for now, with no sword/bayonet moves in the first slice.
- **M1 Garand, squad armorer's rebuild — Dead Reckoning:** balanced stats; consecutive melee hits briefly improve CombinatorCharge gain. A miss or taking a hit breaks the chain.

## Unique weapons

Unique weapons change a play pattern and get a named identity. Keep each effect legible and implementable as a native ability/effect:

- **Last Post (M1 Garand):** a heavy bash that breaks enemy poise returns a small amount of CombinatorCharge. Built around the fallen squad leader; dependable all-rounder.
- **Black Rain (Type 99):** radiation damage leaves a short-lived mark; the next bash against that target consumes the mark for bonus stagger. Rewards alternating spell and melee use.
- **Church Key (M1918A2 BAR):** charged bash sends a short ground pulse that interrupts nearby light enemies. High stamina cost and long recovery keep it from replacing ordinary attacks.

Unique effects should not bypass the 90% bullet reduction. Their special properties apply to melee or radiation damage only.

## Radiation abilities

The Combinator starts with two active skills and one passive unlock. Skill costs and damage are tuned after the first combat prototype.

- **Geiger Bloom — active:** short-range burst that deals modest radiation damage and interrupts a group. Starter crowd-control tool.
- **Hotwire — active:** charge the held weapon; the next two butt strikes add radiation damage and extra poise damage. Teaches melee-spell weaving.
- **Afterimage — passive:** a well-timed dodge grants a brief CombinatorCharge bonus. Unlock from the first locker after the player understands dodging and charge.

Later skills can explore radiation fields, ranged bolts, and exposure tradeoffs. The opening slice should avoid long-range spell spam and keep the rifle-butt loop central.

## Key NPCs

Working names; dialogue and final characterization are open for iteration.

- **Dr. Hana Mori — Combinator contact:** a physicist hiding in the damaged island clinic. After the player reaches her during the tutorial, she installs the Radiation Combinator and explains that it can bind the residual souls left by the mutated. This unlocks soul collection and radiation skills. She is a mission-critical ally with her own goals, not a merchant.
- **Staff Sergeant Ruth Kincaid — quartermaster:** American squad survivor at the first safehouse. Sells and tunes firearms using recovered parts: bash handling, stamina efficiency, poise damage, and later scarce ammunition. She provides the grounded military voice.
- **Aki Tanaka — village boatwright:** survivor who knows the island's routes and shore conditions. Trades recovered parts for healing supplies, temporary radiation protection, and route intel. Their shop expands as safe paths are reopened.

## Tutorial loop

1. Reach the wrecked shore, learn movement, camera control, light bash, and dodge with the M1 Garand.
2. Face a mutated villager: demonstrate that bullets do only 10% damage, while a bash staggers it. A limited shot makes the resistance clear without making shooting the best answer.
3. Reach Dr. Mori at the clinic and receive the Combinator.
4. Fight a small group; collect souls automatically and use Geiger Bloom once charge is granted.
5. Return to the radiation locker safehouse. Teach rest/reset, one level-up, then introduce Kincaid and Tanaka.
6. Leave by a second route that reconnects to the shore approach, closing the starter-level loop and letting the player test the new weapon/skill choice.

## C++ implementation order

1. Split the radiation resource into `CombinatorCharge` and a future `RadiationExposure`; add explicit bullet, bash, and radiation damage types/resistance handling.
2. Add native weapon definitions with the five tuning fields above and native light/heavy bash abilities.
3. Implement Geiger Bloom and Hotwire as C++ Gameplay Abilities with Gameplay Effects; keep costs, cooldowns, and tags in GAS.
4. Add soul pickups, locker level-up/rest behavior, and merchant inventory/purchase logic as C++ actors/components.
5. Assemble the tutorial route from primitive geometry and C++-spawned actors before importing the coastal art pack.
