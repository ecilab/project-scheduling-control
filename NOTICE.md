# Notices

## Name and logo
The **ECI Lab** name, the **ECI** logo (embedded in `index.html`) and related branding are **not** covered by the MIT License. They may not be used in modified or redistributed versions, or to suggest endorsement, without written permission from ECI Lab. If you publish a modified version, please replace the logo and remove the ECI Lab branding.

## Documentation and example data
The files in `docs/` and `examples/` are licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**: https://creativecommons.org/licenses/by/4.0/
You may share and adapt them for any purpose, provided you credit: *Prof. Abdulrahman Al-Ahmari, ECI Lab*.

All example projects are fictional and were written for teaching.

## Third-party resources
The application loads the following fonts from Google Fonts at runtime. They are not included in this repository and are licensed under the SIL Open Font License 1.1:
- Manrope
- Tajawal
- Readex Pro

No third-party JavaScript libraries are used. All charts, diagrams and icons are drawn in SVG inside `index.html`.

## Privacy
The application runs entirely in the browser. By default it sends no project data anywhere; projects, the theme and the language choice are stored only in the visitor's own browser (localStorage).

The optional AI assistant is off by default. When a user turns it on and enters their own API key, the project data and the user's questions are sent to the provider they choose (Anthropic or OpenAI) under that provider's terms, and usage is billed to the user's key. The key is sent only to that provider. It is kept in sessionStorage (forgotten when the tab closes) unless the user chooses to remember it on the device (localStorage).
