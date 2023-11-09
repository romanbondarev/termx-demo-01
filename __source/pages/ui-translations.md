

1. Navigate to the `termx-web/src/assets/i18n` folder in [TermX Web](https://gitlab.com/kodality/ng/marina/-/tree/main/modules/ui/src/locales). 
1. Use the `en.json` file as the source for your translations. Once you've finished, add this file back to the same folder, but with your [language code](https://www.localeplanet.com/icu) (e.g., `et.json`).
1. Include the language translation in `termx-web/app/src/assets/ui-languages.json`.
1. Append your language code to the `UI_LANGS` variable in `termx-web/app/src/environments/environment.base.ts`.

*Ensure the existence of your translations in [Core Utils](https://gitlab.com/kodality/ng/utils/-/tree/main/core-util/lib/locales) and the [Marina](https://gitlab.com/kodality/ng/marina/-/tree/main/modules/ui/src/locales) project.*
