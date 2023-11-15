## Useful CVR Classes for Modders

This page provides a guide to some of the key classes in the game that are useful for modding. Note that these details
may change with game updates. If you find any discrepancies or wish to contribute, you're welcome to submit a Pull
Request.

### CVRGameEventSystem

- **Purpose**: Contains events to attach listeners to, enabling reactions to game happenings.
- **Stability**: Designed for modders; unlikely to break across updates.
- **Usage**: Before patching methods, check here to see if you can react to events directly.

### MetaPort.Instance

- **Purpose**: Stores various settings related to the current game state.
- **Key Properties**:
    - `ownerId` (`string`): Your user id.
    - `isUsingVr` (`bool`): Indicates if the player is in VR (note: this can change at runtime).
    - `CurrentWorldId` (`string`): The id of your current world.
    - `currentAvatarGuid` (`string`): The id of your current avatar.
- **Usage**: A primary reference point for accessing game state information.

### PlayerSetup.Instance

- **Purpose**: Contains extensive information and references related to the local player.

### MovementSystem.Instance

- **Purpose**: Related to player controller actions like movement, flying, sitting, crouch, etc.

### ViewManager.Instance

- **Purpose**: Manages the Main Menu.

### CohtmlHud.Instance

- **Purpose**: Manages the HUD with features like microphone mute, notifications, vote kick icons.

### CVR_MenuManager.Instance

- **Purpose**: Handles all Quick Menu related features.

### CVRPlayerManager.Instance

- **Purpose**: Provides access to remote players, including listing and exposes a references to useful things.
