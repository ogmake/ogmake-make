# make-ogmake

Make custom app definition for [ogmake](https://ogmake.com). Files are plain IML/JSON in the layout the Make Apps editor and the "Make Apps Editor" VS Code extension use.

## Contents
- `base.imljson` - base URL `https://ogmake.com`, bearer auth header, error mapping.
- `connections/ogmake/` - API key connection; test call `GET /v1/usage`.
- `modules/create-image/` - action: `POST /v1/images` (template, fields, format incl. PDF, preset) returns the hosted URL.
- `modules/render-html/` - action: `POST /v1/images` with raw `html`, optional `css`, width, height, format (2 credits).
- `modules/list-templates/` - search: `GET /v1/templates`.

## Import
1. In the Make Apps builder (Custom apps > Create a new app, name `ogmake`), or with the VS Code "Make Apps Editor" extension: "Import from Make", replace the files with these, "Deploy to Make".
2. Create the connection with an og_live_... key, run a module, check the output.
3. Share the app with teammates via its invite link.

Optional `format`/`preset`/`css`/`height`/`fullPage` are omitted from the request when left empty (`ignore`). Support: support@ogmake.com
