# Home Assistant Button Card — Theme-aware fork

This repository is a HACS-compatible fork of [custom-cards/button-card](https://github.com/custom-cards/button-card), originally created by [RomRider](https://github.com/RomRider). It keeps the upstream card's features and adds theme-aware state colors for card backgrounds.

This is an independent fork, not the upstream project. The fork-specific behavior described below applies to the code published in this repository.

## Fork-specific change: use Home Assistant theme state colors

For cards using the card color type, the automatic state background follows Home Assistant's theme state-color variables instead of using a light's RGB or color-temperature color for the card background. This makes active and inactive card backgrounds consistent with the selected HA theme.

With the icon color type, the icon keeps the upstream light-color behavior, including RGB and color-temperature coloring where supported. Explicit colors configured in a card or its state rules continue to take precedence according to the card configuration.

See [Home Assistant theme state colors](https://www.home-assistant.io/integrations/frontend/#themes) and the [complete button-card documentation](https://custom-cards.github.io/button-card/).

## Requirements

- Home Assistant 2025.10.0 or newer.
- HACS, for the recommended installation method.

## Install with HACS (custom repository)

This fork is not part of the HACS default repository list. Add it as a custom repository:

1. In Home Assistant, open **HACS**.
2. Open the **three-dot menu** and choose **Custom repositories**.
3. Enter **ezaekiel/button-card** as the repository.
4. Select **Dashboard** as the category, then add the repository.
5. Find **Button Card** in HACS and download/install it.
6. If HACS asks you to reload Home Assistant or refresh the browser, follow the prompt.

The repository includes the built **button-card.js** file at its root and a **hacs.json** manifest for HACS. If you previously added the repository while it was missing the bundle, refresh HACS and try adding it again.

### Avoid duplicate resources

If the upstream button-card is already installed, do not load both copies as the same **custom:button-card** custom element. Replace the existing resource with this fork, or remove the old installation before adding this one. Keep only one active button-card JavaScript resource in the dashboard.

HACS normally registers the resource automatically. If you need to add it manually, use this URL and resource type:

- URL: **/hacsfiles/button-card/button-card.js**
- Resource type: **JavaScript Module**

## Manual installation

1. Download **button-card.js** from the root of this repository's **master** branch.
2. Copy it to your Home Assistant **www** directory (usually **/config/www/button-card.js**).
3. In **Settings → Dashboards → Resources**, add:
   - URL: **/local/button-card.js**
   - Resource type: **JavaScript Module**
4. Refresh the browser or the Home Assistant companion app.

Do not install both the HACS copy and a manual copy at the same time.

## Use in a dashboard

The custom card type remains:

~~~yaml
type: custom:button-card
entity: light.example
name: Example light
color_type: card
~~~

The fork-specific state background behavior applies when card color is selected. The component retains the upstream configuration options, templates, actions, layouts, and other features. See the [configuration guide](https://custom-cards.github.io/button-card/).

## Build and published bundle

The source code is in **src/**. A GitHub Actions workflow builds the distributable when changes are pushed to **master** and publishes the generated **button-card.js** file at the repository root for HACS. The checked-in root bundle is the file HACS installs; editing source files alone does not change the installed card until a new bundle is generated.

## Upstream project and license

- Upstream project: [custom-cards/button-card](https://github.com/custom-cards/button-card)
- Upstream documentation: [button-card documentation](https://custom-cards.github.io/button-card/)
- License: [MIT](LICENSE.md)

Please use this repository's issues for fork-specific bugs. For behavior unchanged from upstream, consult the upstream documentation and community resources.
