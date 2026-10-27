# Addons in die eine Create-Jar einbauen

Ziel: Beim Kompilieren (`./gradlew build`) entsteht **eine einzige** Create-Jar, die alle Addons aus `roh/` enthält.

## Layout
```
roh/
  dependencies.gradle        (optional) zusätzliche Maven-Repos/Abhängigkeiten der Addons
  <addon>/src/main/java      -> wird Teil des main-Source-Sets
  <addon>/src/main/resources -> wird nach build/roh-resources kopiert und in die Jar aufgenommen
```
Pro Addon muss nur `src/main/java` (und `src/main/resources`) vorhanden sein. Ein eigenes Gradle-Projekt wird nicht gebaut.

## Was automatisch passiert (`build.gradle`)
- Java-Quellen aller `roh/<addon>/src/main/java` werden mitkompiliert.
- Ressourcen werden über den Task `stageRohResources` zusammengeführt. **Doppelte Dateien zwischen Addons lassen den Build fehlschlagen** (kein stilles Überschreiben).
- Nicht übernommen, aber beim Build als Warnung gemeldet: `META-INF/neoforge.mods.toml`, `META-INF/mods.toml`, `META-INF/accesstransformer.cfg`, `pack.mcmeta`, `icon.png`, `mcmod.info`.

## Was pro Addon manuell nötig bleibt
1. **Mod-Metadaten:** `@Mod("<addonid>")`-Klassen brauchen einen `[[mods]]`-Block (plus Abhängigkeiten) in `src/main/templates/META-INF/neoforge.mods.toml`, sonst lädt NeoForge sie nicht. Alternativ den Einstieg in `Create.java` aufrufen und die `@Mod`-Annotation entfernen.
2. **Mixins:** Mixin-JSONs der Addons als zusätzliche `[[mixins]]`-Einträge eintragen; Paketnamen dürfen nicht kollidieren.
3. **Access Transformer:** Einträge in `src/main/resources/META-INF/accesstransformer.cfg` zusammenführen.
4. **Abhängigkeiten:** Bibliotheken/Mods, die Addons brauchen, in `roh/dependencies.gradle` (`jarJar`/`implementation`).
5. **Paketkonflikte:** Gleiche voll qualifizierte Klassennamen in mehreren Addons führen zu Kompilierfehlern und müssen aufgelöst werden.

## Verifiziert
Mit einem Dummy-Addon (Klasse + Asset + eigener `pack.mcmeta`) lief `./gradlew jar` erfolgreich; die Jar enthielt Klasse und Asset, die `pack.mcmeta` von Create blieb erhalten. Das Dummy-Addon wurde wieder entfernt. Mit echten Addons ist nichts getestet.
