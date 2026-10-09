# Game Engines Midterm

## Implementations

### Factory Pattern (demonstrates polymorphism)

The `BP_Factory` Blueprint is responsible for spawning in projectiles shot by the player. It remains unaware of what type of bullet (or bubble) to spawn in, and simply calls the `spawnBullet` function when `G` is pressed.

<img height="600" src="https://github.com/user-attachments/assets/1544ef15-0419-4cc2-b24e-01e617dc1221" />

### Singleton Pattern (demonstrates encapsulation)

The `GI_UIManager` GameInstance is a singleton Blueprint responsible for managing the onscreen score counter. It does this by declaring `getScore` and `addScore`, which encapsulate the `score` variable, which is also part of `GI_UIManager`. This blueprint also has a wrapper function for the *Spawn Actor from Class* node, named `spawnBullet`, which is used in the Factory pattern above.

#### `getScore` function
<img height="200" src="https://github.com/user-attachments/assets/47cb657e-5fa1-4882-be98-1407b8b6340a" />

#### `addScore` function
<img height="200" src="https://github.com/user-attachments/assets/17dc49a1-c1c0-4d37-8ee3-8a4a61d61b14" />

#### `spawnBullet` function
<img height="160" src="https://github.com/user-attachments/assets/468b7494-8e2f-4105-b5b2-3eab623ae042" />

### Widget blueprint (Score counter UI)

The `BP_UserInterface` Blueprint is responsible for displaying the UI on the screen (it gets initialized by the level blueprint, shown below).

<img height="120" src="https://github.com/user-attachments/assets/b03555af-86fc-49ee-b98c-009e84999a98" />

The binding for the Score text is a function (auto-named `GetText`) that live fetches the value from the Singleton `GI_UIManager`.

<img height="200" src="https://github.com/user-attachments/assets/56b31bde-f4e9-42e4-b864-8d48933c13d9" />

### Enemy blueprint

The `enemy` Blueprint contains the code for the enemy chasing the player. It does this by rotating itself toward the player and adding an impulse of its forward vector. This results in a very goofy-looking, yet effective enemy chasing mechanic, where the enemy sort of just magnetizes toward the player.

<img height="200" src="https://github.com/user-attachments/assets/2504d368-3ac7-45bc-aea7-c757eae78cc3" />

### Child enemy blueprint (demonstrates inheritance)

The `childEnemy` Blueprint is a child class of the `enemy` Blueprint, and a literal child enemy. It inherits all the behavior and components of the `enemy` Blueprint, except the mesh is scaled to 0.5x.

<img height="200" src="https://github.com/user-attachments/assets/d833d184-abac-4453-8694-46efdb2d4ca2" />

## What went wrong or wasn't implemented, and how I would change it

Unfortunately, a lot of things went wrong in the <60 minutes that this project was being worked on. Below is a list of every known issue with the final build, and how I would've fixed it, given enough time.

- Gaps in enemy implementation
  - Enemies can't die, and as a result, score stagnates (I'd fix by implementing enemy death using *Destroy Actor* node and update score using `addScore` from `GI_UIManager`.)
  - Enemies cannot harm the player (I'd fix by setting up 3 life system for the player, giving them invincibility frames, and making a UI Widget for a win and loss screen).
- Platforms on map aren't set up well. (I'd fix by properly building environment, given enough time)
- Projectile motion doesn't work properyl. (I'd fix by debugging the issue with the *Add Impulse* node, given enough time)
