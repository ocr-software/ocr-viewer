# OCR viewer: word boxes, confidence and layout for OCR results, in any web page

Show an OCR result on top of the page image: every word in its box, how sure the OCR is about it, and the layout. One JavaScript file, one CSS file, no other library. For results from the [ocr-software.com](https://ocr-software.com/) API.

![OCR viewer showing an invoice with the field "total" and its word box highlighted](screenshot-extract.png)

## What it shows

- **Word boxes.** Each word sits in its box on the page image. A click on a word or a field shows where it came from.
- **Confidence.** Every word carries a value from 0 to 1. Set a threshold and the viewer marks the words below it.
- **Layout.** Lines, blocks and tables, as the service found them, plus the text, formatted text, hOCR and JSON of the same page.
- **Extract, Split and Classify (Preview, free, quality still improving).** Give the service a schema and get fields back, each with its word boxes as proof. A field without proof on the page is marked, never filled in. Split cuts a stack of pages into documents, Classify names the document type. Expect mistakes and check what matters.

## Quick start

You need a result from the API and the page image. The viewer does not read documents itself.

```sh
curl -s -X POST "https://api.ocr-software.com/v1/jobs?pipeline=scan-ctc@2&formats=json" -H "Authorization: Bearer $OCR_KEY" --data-binary @page.pdf   # note the job_id
curl -s "https://api.ocr-software.com/v1/jobs/$JOB_ID/result?format=json" -H "Authorization: Bearer $OCR_KEY" -o result.json   # when the job is done
```

```html
<link rel="stylesheet" href="ocr-viewer.css"><div id="v"></div><script src="ocr-viewer.js"></script>
<script>OcrViewer.mount(document.getElementById("v"), {result: "result.json", image: "page.png"});</script>
```

`example.html` is the whole thing with sample data. Serve this folder over http (`python -m http.server`); a browser does not load the JSON files from `file://`.

## You need a key

The API needs a key. It is free: get one at [ocr-software.com/order/](https://ocr-software.com/order/). Never put the key in a public page. Fetch the result on your server and hand the viewer the JSON. Don't have a key yet? [Try one page without one](https://ocr-software.com/try/).

## Docs and test

- [API documentation](https://ocr-software.com/docs/)
- [Try a page in the browser](https://ocr-software.com/try/)

## License

AGPL-3.0, see `LICENSE`. A commercial license is available on request via [ocr-software.com](https://ocr-software.com/).

## Provider and legal

The service is operated by Helm & Nagel GmbH. [Terms](https://ocr-software.com/legal/saas-terms/) · [Privacy](https://ocr-software.com/legal/privacy/) · [Imprint](https://ocr-software.com/legal/imprint/) · [Security](https://ocr-software.com/legal/security/)
