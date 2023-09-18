# README

**Benchmark**: SLOW: 3-6s and styles are cached (no live reload)
**Asset pipeline:** propshaft, importmaps
**Technologies:** foreman, assets bundling with node, bootstrap from node_modules

I am trying to choose the best of at least approproate Asset Pipeline for my apps.

The project is using Bootstrap 5, not so much for styles and perks, but mainly because it illustrates the use of external library with JS and CSS components. JS part has dependency on popper.js and CSS part has optional config for Sass.

| Technology                   | Description  |
| ---------------------------- | ------------ |
| Asset Pipeline               | propshaft    |
| Bootstrap                    | npm          |
| Sass compiling/ minification | yarn sass    |
| JS minification/bundling     | yarn esbuild |
| Naming                       | importmaps   |
| Bundling                     | yarn esbuild |

### Basic needs for a quick start

- Bundled and minified Bootstrap 5: from npm module
- Sass compilation / minification: by Node’s DartSass
- `cssbulding-rails` gem is not doing any job, it is a stub for installing Node’s DartSass
- JS bundling: done by Node’s esbuild
- `jsbundling-rails` gem is not doing any job, it is a stub for installing Node’s esbuild
- Assets fingerprinting: Propshaft

#### JS handling

Importmaps is included. It allows simpler reference providing a nickname to imported JS assets (whether CDN or gem or vendor folder or local folder). JS libraries have to be modularized. References can be quickly swapped (say, from gem to CDN) without changing a nickname.
JS source folder with umninified, unbundled assets is currently under `app/javascript`, not `app/assets/javascript`.

#### CSS handling

If you have to have Sass, you need to use dartsass-rails or sassc-rails. Otherwise, CSS is handled by the Asset Pipeline.

#### Asset Pipeline

Propshaft does not minify assets, it only handles assets paths and digital stamping / fingerprinting. Since if handles paths, it decodes `url(asset)` to `url(digested-asset)` in CSS files. Apparently CSS files do not have to be ERB for that to work.
