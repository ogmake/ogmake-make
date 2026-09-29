# make-ogmake

Make custom app definition for [ogmake](https://ogmake.com). Files are plain IML/JSON in the layout the Make Apps editor and the "Make Apps Editor" VS Code extension use.

## Contents
- `base.imljson` - base URL `https://ogmake.com`, bearer auth header, error mapping.
- `connections/ogmake/` - API key connection; test call `GET /v1/usage`.
- `modules/create-image/` - action: `POST /v1/images` (template, fields, format incl. PDF, preset) returns the hosted URL.
- `modules/render-html/` - action: `POST /v1/images` with raw `html`, optional `css`, width, height, format (2 credits).
- `modules/screenshot/` - action: `POST /v1/screenshot` (url, width, height, full page, format; 3 credits).
- `modules/list-templates/` - search: `GET /v1/templates`.

## Not included
- **Build Signed URL**: needs HMAC-SHA256 over a base64-decoded secret with base64url output; Make IML cannot decode a base64 key for `sha256(text; encoding; key)`, so it is not implementable honestly. Use Create Image (hosted URL), or sign in a code step / the n8n or Zapier apps.
- **Check URL**: `/v1/check` is admin-gated, not in the public API.

## Import (not done; unverified against a live Make account)
1. Make account with access to https://www.make.com/en/api-documentation custom apps (Apps builder in the dashboard: Custom apps > Create a new app, name `ogmake`, private).
2. Preferred: install the VS Code "Make Apps Editor" extension, sign in, "Import from Make", then replace the imported files with these and "Deploy to Make". Otherwise paste each file into the matching tab in the web editor: Base, Connections > Communication/Parameters, Modules > Communication/Mappable parameters/Interface.
3. Create the connection with an og_live_... key, run the module, check the output.
4. Make requires review by Make to publish publicly; a private app can be shared by invite link.

Optional `format`/`preset`/`css`/`height`/`fullPage` are omitted from the request when left empty (`ignore`). Support: support@ogmake.com
