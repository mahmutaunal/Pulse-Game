# PULSE

**Understand the network. Guide the energy. Bring worlds back to life.**

PULSE is a closed-source puzzle game for Android and iOS, built with Unity 6. It combines logical deduction, progressive discovery, and radial energy propagation: read the clues, change the network, and deliver energy to its targets to restore the ORIGIN system.

![PULSE promotional artwork: a glowing energy network with the Turkish tagline “Solve the network. Awaken the energy.”](Assets/StoreListing/Pulse-GooglePlay-FeatureGraphic-TR-1024x500.png)

This private repository contains the Unity project, original assets, frozen campaign content, development tools, and tests. The current focus is preparing the existing game for Google Play closed testing. Further product development is not currently planned by the owner.

## At a glance

| Item | Configuration |
| --- | --- |
| Engine | **Unity 6000.6.3f1**, C#, URP / Universal 2D with selected 3D presentation |
| Platforms | Android and iOS, portrait orientation |
| Internal version | `0.1.0` |
| Application identifier | `com.alpwarestudio.pulse` on both platforms |
| Root namespace | `AlpWare.Pulse` |
| Main scene | `Assets/_Pulse/Scenes/Consumer.unity` |
| Campaign | **80 levels across five worlds** in ORIGIN |
| Persistence | Local progress, preferences, and interrupted-run recovery |
| License | Proprietary; third-party components retain their own licenses |

PULSE is the current project name and product placeholder. Legal notices use the owner-supplied publisher name **AlpWaare Studio**. The existing Unity company field, `AlpWare Studio`, namespaces, folders, and platform identifiers are preserved.

## In-game gallery

The following images combine actual Unity Editor captures of the Consumer scene with Turkish promotional headings. The in-game interface supports English and Turkish; switch languages in Settings. Before a manual choice, Turkish devices start in Turkish and all other device languages start in English. A manual language choice is saved for the next launch. The banner above is promotional illustration; the gallery below shows the implemented game.

<table>
  <tr>
    <td width="25%"><a href="Assets/StoreListing/Pulse-Store-TR-01-Dunyayi-Uyandir-1080x1920.png"><img src="Assets/StoreListing/Pulse-Store-TR-01-Dunyayi-Uyandir-1080x1920.png" alt="ORIGIN galaxy view with the Turkish heading: Awaken a world" width="240"></a></td>
    <td width="25%"><a href="Assets/StoreListing/Pulse-Store-TR-02-Yolunu-Kesfet-1080x1920.png"><img src="Assets/StoreListing/Pulse-Store-TR-02-Yolunu-Kesfet-1080x1920.png" alt="AURELIA sector map with the Turkish heading: Discover your path" width="240"></a></td>
    <td width="25%"><a href="Assets/StoreListing/Pulse-Store-TR-03-Bolumleri-Kesfet-1080x1920.png"><img src="Assets/StoreListing/Pulse-Store-TR-03-Bolumleri-Kesfet-1080x1920.png" alt="AURELIA sector entry with the Turkish heading: A new connection in every level" width="240"></a></td>
    <td width="25%"><a href="Assets/StoreListing/Pulse-Store-TR-04-Agi-Coz-1080x1920.png"><img src="Assets/StoreListing/Pulse-Store-TR-04-Agi-Coz-1080x1920.png" alt="AURELIA 7 puzzle with the Turkish heading: Read the clues. Solve the network." width="240"></a></td>
  </tr>
  <tr>
    <td align="center">Explore ORIGIN</td>
    <td align="center">Choose a sector</td>
    <td align="center">Enter the network</td>
    <td align="center">Solve the puzzle</td>
  </tr>
</table>

Each gallery image is available at 1080 × 1920. Click an image to open the full-size asset. All artwork is stored in [Assets/StoreListing](Assets/StoreListing/), including the [application icon](Assets/StoreListing/Pulse-GooglePlay-Icon-512.png). These existing image files have been embedded without modification.

## Gameplay

Explore **AURELIA, VESPER, HELION, UMBRA, and ECHO**, each containing sixteen prepared levels. Campaign definitions are frozen: levels are loaded directly, without runtime generation or solver searches.

- **Tap** to scan, send a Pulse from a ready powered node, or change a visible Switch's route, depending on the node's state.
- **Hold** to isolate a node or reverse its isolation.
- **Observe** Signals, power, and visible connections together. Powered discovery boundaries reveal new information.
- **Restore** Targets and advance world restoration. Optional Mastery objectives never gate ordinary progression.

The central design principle is **known information → justified action → new information**. The simulation is deterministic: identical initial state and actions produce identical results. Energy and related offers are hidden throughout the first ten campaign levels; their retries and restarts are free.

## Getting started

### Requirements

- Authorized repository access, Git, and Git LFS for the creative source formats configured in `.gitattributes`.
- Unity Hub and **Unity 6000.6.3f1**, as pinned in [ProjectVersion.txt](ProjectSettings/ProjectVersion.txt).
- For Android builds: Android Build Support and the corresponding SDK, NDK, and OpenJDK components.
- For iOS builds: macOS, iOS Build Support, and an appropriate Xcode and signing environment.

### Open and run

1. Obtain an authorized checkout. With Git LFS installed, run `git lfs install` and `git lfs pull` from the repository root.
2. Add the repository root to Unity Hub. `Assets`, `Packages`, and `ProjectSettings` must remain together.
3. Open with the pinned Editor and wait for package resolution and asset import. Preserve the existing engine and package versions.
4. With Play Mode stopped, choose **PULSE → Consumer Experience (Task 010B)**, or open `Assets/_Pulse/Scenes/Consumer.unity` directly.
5. Select a portrait Game view and enter Play Mode.

Generated caches, logs, temporary Android files, IDE project files, and local builds are excluded from Git. A fresh checkout may need internet access and additional time to download packages and rebuild `Library`. Dependencies are recorded in [manifest.json](Packages/manifest.json) and [packages-lock.json](Packages/packages-lock.json).

Startup uses a static PULSE splash on Android and iOS, with a matching iOS launch screen and Consumer boot handoff. See [splash assets and validation](Tools/Splash/README.md).

### Scenes

| Scene | Purpose |
| --- | --- |
| `Consumer.unity` | Main player experience: home, resume, world navigation, puzzles, and results |
| `Gameplay.unity` | First-ten baseline and regression reference |
| `DecisionVariety.unity` | Separate A–E decision-variety experiments |
| `OriginCampaign.unity` | Frozen campaign inspection |
| `ProductSystems.unity` | Save, progression, economy, and mock-provider validation |
| `LegacyGameplay.unity` | Historical v1 diagnostics |

The shared [build scene list](ProjectSettings/EditorBuildSettings.asset) includes **Consumer first and Gameplay second**, both enabled. The other scenes are development references outside that list.

## Architecture

Core owns deterministic rules, geometry, state, and events. Application manages progression and product transactions. Presentation consumes player-visible views and events; visual effects and Unity Physics do not determine puzzle outcomes.

| Directory | Responsibility |
| --- | --- |
| `Assets/_Pulse/Core/` | Deterministic network simulation, rules, geometry, and events |
| `Assets/_Pulse/Levels/` | Schemas, reference content, and frozen ORIGIN campaign |
| `Assets/_Pulse/Application/` | Sessions, progression, persistence, Energy, hints, and provider interfaces |
| `Assets/_Pulse/Presentation/` | Rendering, input, world presentation, audio/haptic orchestration |
| `Assets/_Pulse/UI/` and `Assets/_Pulse/Audio/` | UI components, typography, styling, and audio assets |
| `Assets/_Pulse/Solver/` and `Assets/_Pulse/LevelFactory/` | Offline solving, generation, and content validation |
| `Assets/_Pulse/Editor/` | Editor tools and development entry points |
| `Assets/_Pulse/Tests/` | EditMode and PlayMode regression tests |
| `Assets/Plugins/` | Platform integrations and Android release configuration |
| `Assets/StoreListing/` | App icon, feature graphic, and store gallery images |
| `Tools/OriginCampaign/` | Offline campaign production recipes and tooling |
| `Packages/` and `ProjectSettings/` | Shared dependencies and Unity project configuration |
| `docs/index.html` | Shared Android/iOS privacy policy |

Solver and Factory are development tools, not runtime gameplay authorities. Do not regenerate the accepted campaign merely to verify it or replace frozen level identifiers. See the [offline production tool notes](Tools/OriginCampaign/README.md).

## Saves and services

Saves are held under `Application.persistentDataPath`:

- **Release composition:** `pulse-product-v1.save`.
- **DEBUG composition:** `pulse-product-development-v1.save`, with development clock controls, mock ad/purchase providers, and local analytics logging.

The save system maintains a previous-generation `.bak` and checks integrity. Integrity checking is not encryption. Development and release save files are separate; mock success does not represent a real advertisement or payment.

The release composition currently uses unavailable ad/purchase adapters and a no-op product analytics provider. There is no game account server or game-managed cloud synchronization. Campaign play works offline. Operating-system backups and Unity engine diagnostics are separate concerns: the in-game analytics toggle defaults to on for new installations and does not disable engine diagnostics. Previously saved choices are preserved, and players can turn product analytics off in Settings. Data practices are described in the [privacy policy](docs/index.html).

## Android release preparation

The Android release profile uses IL2CPP and ARM64. Release R8 minification and Android resource shrinking are configured, with project-specific ProGuard additions and native symbol output. Managed stripping has not been made more aggressive. See [Android release build notes](Assets/Plugins/Android/RELEASE_BUILD_NOTES.md) for configuration, validation results, and outstanding checks.

For each upload, retain the exact AAB, R8 mapping, and native symbols together outside Git. Use your existing release keystore and a previously unused Bundle Version Code. Signing material and passwords must remain outside version control.

Closed-test release acceptance still requires a fresh signed build and real-device checks for launch, input, save recovery, navigation, audio/haptics, stability, and performance. Store age declarations, privacy disclosures, a public HTTPS policy URL, in-app policy access, and distribution of third-party notices must match the actual release. This README does not certify store approval or device acceptance.

## Verification

Use a directly affected test or narrow fixture when validating gameplay/system changes. Full EditMode, PlayMode, and domain suites remain deferred to owner validation. A successful compilation is not a passed runtime test.

This README update was checked for local links, gallery references, and unchanged image hashes. No gameplay tests, Unity import, or player builds were run for this documentation change.

**FULL TEST SUITE: NOT RUN — DEFERRED TO OWNER VALIDATION.**

Repository instructions are maintained in [AGENTS.md](AGENTS.md). Earlier production specifications and milestone reports were removed at the owner's request; this README links only to documentation currently present in the checkout.

## License and contact

**© 2026 AlpWaare Studio. All rights reserved.** Original project materials are proprietary. Repository access does not grant permission to redistribute them or reuse them in another project. See [LICENSE](LICENSE).

Third-party components remain subject to their respective terms: [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt). The [privacy policy file](docs/index.html) contains Turkish and English text; its repository link is not a substitute for a publicly hosted store policy URL.

**Contact:** [contact@alpwarestudio.com](mailto:contact@alpwarestudio.com) · Türkiye
