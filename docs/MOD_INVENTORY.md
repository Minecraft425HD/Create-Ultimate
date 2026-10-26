# Create Ultimate – Bestandsaufnahme (Stand: Etappe 0)

## Projektumgebung (aus den tatsächlichen Dateien)

| Eigenschaft | Wert | Quelle |
|---|---|---|
| Mod-ID / Name | `create` / Create | gradle.properties |
| Mod-Version | 6.0.11 | gradle.properties |
| Minecraft | 1.21.1 | gradle.properties |
| NeoForge | 21.1.219 | gradle.properties |
| Mappings | Parchment 2024.11.17 | gradle.properties |
| Java | 21 (Toolchain; lokal OpenJDK 21.0.12) | build.gradle |
| Gradle | 8.14.3 (Wrapper) | gradle-wrapper.properties |
| Build-Plugins | ModDevGradle 2.0.141, Blossom, Silk, mod-publish-plugin | build.gradle |
| Registrate | MC1.21-1.3.0+67 (jarJar) | gradle.properties |
| Ponder / Flywheel / Vanillin | 1.0.85 / 1.0.6 / 1.1.3-41 | gradle.properties |
| Optional/Compat | JEI 19.21.0.247, Curios 9.2.2, Sodium 0.6.9, CC:Tweaked 1.116.1, Farmer's Delight 1.2.9 | gradle.properties |
| Quellcode | ~2017 Java-Dateien in `src/main/java`, Ressourcen in `src/main/resources`, generierte Daten in `src/generated` | Dateisystem |
| Tests | Keine JUnit-Tests; NeoForge-GameTests in `infrastructure/gametest` (Namespace `create`) | Dateisystem |

## Ordner `roh`

**Nicht vorhanden.** Weder im Dateisystem der Sitzung noch im Git-Baum von `origin/main` oder
`origin/claude/awesome-ride-yznfvl` (Create-Ultimate) gibt es einen Ordner `roh`. Das Repository
`Async-Programming` enthält nur `LICENSE` und `README.md`. Es gibt daher aktuell **keine Addon-Mods
zu inventarisieren oder zu integrieren**.

| Mod | Analysiert | Integriert | Kompiliert | Tests | SP | Server | MP |
|---|---|---|---|---|---|---|---|
| Create (Basis, 6.0.11) | Teilweise (Build/Metadaten) | n/a (Referenz) | Ja | Nicht ausgeführt | Nein | Nein | Nein |
| Addons aus `roh` | Nein (Quelle fehlt) | Nein | – | – | – | – | – |

## Baseline-Prüfungen (tatsächlich ausgeführt)

- `./gradlew help` → BUILD SUCCESSFUL (31 s)
- `./gradlew compileJava` → BUILD SUCCESSFUL (4 m 41 s), 66 Compiler-Warnungen (Deprecation/Removal-Hinweise, u. a. `FluidIngredientOld`, `BlockBuilder.addLayer`), keine Fehler.
- Nicht ausgeführt: GameTests (`runGameTestServer`), Client-/Server-Start, Multiplayer.

## Vorgefundene Auffälligkeiten

1. Kein `.gitignore` → `build/` und `.gradle/` erscheinen als untracked.
2. `AGENTS.md` (Upstream) enthält eine "No-LLM"-Policy der Create-Maintainer. Lizenz-/Policy-Lage
   für Addon-Quellcode ist vor einer Weitergabe separat zu klären (`LICENSE.md`).
3. `settings.gradle` bindet `Ponder` als includeBuild nur ein, wenn der Ordner existiert (aktuell nicht).

## Nächster Schritt

`roh` mit den Addon-Quellen bereitstellen (z. B. committen unter `Create-Ultimate/roh/<modname>/`).
Danach: rekursive Inventarisierung, Abhängigkeitsanalyse, Integrationsreihenfolge.
