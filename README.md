# Radiation Coast — Native GAS starter

C++-only Unreal Engine 5 Gameplay Ability System foundation for a third-person action RPG. No Blueprint classes or assets are required by this starter.

## First backend slice

- Replicated GAS attributes: Health, Stamina, Radiation, Souls, Level, and incoming damage.
- A character-owned Ability System Component with the character as both owner and avatar, suitable for a single-player prototype and ready for replication.
- Attribute clamping and Health-zero handling hooks.
- Soul award and level-up logic centralized in the character progression API. Locker checkpoint/rest interactions can be added without moving progression rules into UI or Blueprint.
- Native ability classes can be granted from C++ defaults once the first combat actions are defined.

## Integration

The C++ module and project descriptor are being prepared for UE 5.8. The first slice deliberately has no content assets, maps, input setup, UI, or animation dependencies. The next implementation slice is a native rifle-butt melee ability that traces a short hit window and applies Gameplay Effect damage; weapon damage and the villagers' bullet resistance should be separate damage channels/effect rules.
