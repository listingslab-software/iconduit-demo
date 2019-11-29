## base64

Encode graphic inputs into a single config JSON Object

Includes an example `iconduit.config.json` which incorporates a PNG as encoded base 64 and SVGs converted into JSON in a directory called `/input/base64`.

The JSON object aims to describe everything Iconduit needs. This example includes a 4096px square icon which has encoded as Base 64, which is why it's a ginormous 1mb in size.

SVGs have been converted into JSON using [svgson](https://github.com/elrumordelaluz/svgson-cli)

In theory if we encode binary images as [Base 64](https://en.wikipedia.org/wiki/Base64#Design), and SVG as normalised JSON, they can be incorporated into a JSON object which can be POSTed to a RESTful endpoint or saved into a noSQL DB.

### Example

`/input/base64/inconduit.inputs.json`

```javascript
{
    "name": "Base 64 Encoded Graphics",
    "shortName": "Base64",
    "description": "Lorem Ipsum",
    "displayMode": "fullscreen",
    "outputPath": "./",
    "urls": {
        "base": "https://iconduit.github.io/demo/base64/"
    },
    "colors": {
        "brand": "#D5415C"
    },
    "assets": {
        "icon": {
            "png4096": "<https://url>/icon4096.png",
            "base64": "icondata: image / png; base64, iVBORw0KGgoAAAANSUhEUgAAEAAAABAACAYAAADyoyQXAAABG2lUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4KPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iWE1QIENvcmUgNS41LjAiPgogPHJkZjpSREYgeG1sbnM6cmRmPSJod...."
        },
        "svg": {
            "iconBackground": "<svg ..... />",
            "iconBleed": "<svg ..... />",
            "iconFlatForeground": "<svg ..... />",
            "iconSilhouette": "<svg ..... />",
        }
    },
    "loadsMoreConfigOptions": {}
}
```

### Q&A

- How __is__ JSON usually defined?

I'm not sure how definining these kind of objects would normally be done. This first cut of an object is based on the original config object. It is backwards compatable so that any attributes I don't know about or haven't included yet can easily be added when required.

- About Base 64 Images

Base 64 encoding is basically a way of encoding arbitrary binary data in ASCII text. It takes 4 characters per 3 bytes of data, plus potentially a bit of padding at the end. [Encoding and decoding is easy](https://www.base64-image.de) and can be done client side or in node. 

- About SVG in JSON

SVG are going to contain all kinds of annoying characters, attributes and other things which will try extra hard to break Iconduit, so robust encoding is needed. [<svg/son](https://github.com/elrumordelaluz/svgson) looks good.
