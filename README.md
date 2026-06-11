# AliveNpcs EC - Pelican Town Mayor

Official standalone Experimental Content package for AliveNpcs.

This package adds **Mayor Mode**:

- NPCs treat the farmer as Pelican Town's new mayor.
- The premise is only a perception layer for dialogue and scene flavor.
- It does not change vanilla canon, save state, laws, elections, or permanent lore.
- It adds the dialogue action **Ask about mandate** / **Perguntar do mandato** when the mode is active.

## Requirements

- Stardew Valley
- SMAPI
- AliveNpcs `1.3.2` or newer

## Install

Copy this whole folder into your Stardew Valley `Mods` folder:

```text
Mods/
  alive-npcs-ec-pelican-town-mayor/
    manifest.json
    alive-npcs-ec.json
    prompts/
    scenes/
    i18n/
```

Then open the AliveNpcs Experimental Content settings and select **Mayor Mode**.

## No Build Step

This is a content-only AliveNpcs EC package. There is no DLL and no build command.

To change behavior, edit:

- `alive-npcs-ec.json` for ids, mode metadata, actions, and scene directories.
- `prompts/pelican_town_mayor.txt` for the mode prompt.
- `prompts/ask_mandate.txt` for the action prompt.
- `i18n/*.json` for visible labels and scene text.
- `scenes/pelican_town_mayor/intro.json` for the intro scene definition.

Restart the game after edits.

## IDs

Main mode id:

```text
Lucas.AliveNpcs.EC.PelicanTownMayor/Mayor
```

Legacy alias:

```text
PelicanTownMayor
```

Dialogue action:

```text
Lucas.AliveNpcs.EC.PelicanTownMayor/AskMandate
```

Intro scene:

```text
Lucas.AliveNpcs.EC.PelicanTownMayor.scene.intro
```

## License

MIT. See `LICENSE`.
