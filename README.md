HTML5 Security Cheatsheet
====

This is the home of the H5SC or HTML5 Security Cheatsheet. Here you will find three things:

 * A collection of HTML5 related XSS attack vectors
 * A set of useful files for XSS testing
 * A set of formerly hidden features useful for XSS testing

## Project status

The H5SC is an archive, kept online and readable on purpose. The 149 vectors were collected and
verified between 2010 and 2016, with the last additions in 2022. They document how browsers behaved
in that period, and that is the value of the collection: a large share of what sanitizers, filters
and browsers do today exists because of what is catalogued here.

What this means in practice:

 * The `browsers` field of each vector describes the engines of its day. "latest" means "latest
   as of when the vector was verified", not "current". Internet Explorer, Presto-era Opera, E4X,
   XBL, `behavior:` and VML entries describe engines that no longer ship, but still turn up in
   mail clients, embedded webviews and legacy sanitizer code.
 * Vectors are not re-verified against current browsers and there are no plans to re-verify them.
   Entries are not removed either. A vector that stopped working is still a record of a
   parser behaviour that once existed and may exist again elsewhere.
 * New vectors are accepted when they are of the same kind as the collection: a single markup
   snippet that executes script in a named engine, with a reporter credit.

For a living, engine-verified list of XSS payloads see PortSwigger's
[Cross-Site Scripting cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet).
For the reasoning behind attack classes rather than individual payloads, see the DOMPurify wiki page
[Attack Classes & Bypass History](https://github.com/cure53/DOMPurify/wiki/Attack-Classes-&-Bypass-History).
For markup that causes requests rather than script execution, see [HTTPLeaks](https://github.com/cure53/HTTPLeaks).

## The XSS Vectors

The collection of XSS vectors can be found here: https://html5sec.org/

The data lives in this repository as plain JavaScript modules and can be used without the site:

 * `items.js` - the 149 vectors with name, payload, description, fix advice, browser matrix,
   tags and reporter, in seven languages (en, ja, ru, cs, de, tr, zh; not every entry has every
   translation).
 * `payloads.js` - the `%js_alert%`-style placeholders the vectors are written against, so the
   same vector can be rendered with an `alert`, a `confirm`, or your own probe.
 * `categories.js` - the category labels.
 * `vectors.txt` - all vectors in one text file for easy copy and paste.

`lib/index.js` exposes all three as a CommonJS module.

## Useful Files

We published a list of files useful for XSS testing in various situations. They are served from
https://html5sec.org/ and stored in the `/attachments` sub-folder of this repository:

 * https://html5sec.org/test.asf
 * https://html5sec.org/test.avi
 * https://html5sec.org/test.css
 * https://html5sec.org/test.dtd
 * https://html5sec.org/test.eml
 * https://html5sec.org/test.evt
 * https://html5sec.org/test.gif
 * https://html5sec.org/test.hlp
 * https://html5sec.org/test.hta
 * https://html5sec.org/test.htc
 * https://html5sec.org/test.html
 * https://html5sec.org/test.jar
 * https://html5sec.org/test.js
 * https://html5sec.org/test.json
 * https://html5sec.org/test.mpeg
 * https://html5sec.org/test.pdf
 * https://html5sec.org/test.sct
 * https://html5sec.org/test.svg
 * https://html5sec.org/test.swf
 * https://html5sec.org/test.vbs
 * https://html5sec.org/test.vml
 * https://html5sec.org/test.wbxml
 * https://html5sec.org/test.xbl
 * https://html5sec.org/test.xdr
 * https://html5sec.org/test.xml
 * https://html5sec.org/test.xsl
 * https://html5sec.org/test.xxe
 * https://html5sec.org/test.zip
 * https://html5sec.org/Test.class

Pull requests welcome.

## Hidden Features

The H5SC has a few "hidden" features on https://html5sec.org/:

 * An RSS mode to test feed readers: https://html5sec.org/rss
  * `/rss/+/` gives a unix timestamp 300 seconds in future (for ease use)
  * `/rss/+123/` gives a unix timestamp 123 seconds in future
  * `/rss/1234/` will serve a minimal rss feed until unix time is 1234.
 * A JavaScript function to return all vectors as string, isolated and numbered: Go [here](https://html5sec.org/) and execute `vectors()`
 * All H5SC vectors in [one text file](https://raw.githubusercontent.com/cure53/H5SC/master/vectors.txt) for easy copy & paste
 * A useful search API via GET
  * Want all vectors related to `innerHTML`? Open https://html5sec.org/?innerHTML
  * Want to link a specific vector? Open https://html5sec.org/#123
 * A redirect API resolving to a URL containing XSS payload
  *  Data URI, no special status: https://html5sec.org/r/data/
  *  Data URI, status code `307`: https://html5sec.org/r/data/307
  *  JavaScript URI, status code `301`: https://html5sec.org/r/javascript/301
  *  Supported status codes are: `301`, `302`, `303`, `307`, `308`, `999`
  *  Supported schemes are: `data`, `javascript`, `jar`, `script` (redirecting to https://html5sec.org/%3cscript>alert(1)%3c/script>/)

## Contributing

If you have a vector that belongs here, open a pull request against `items.js`. Copy the shape of an
existing entry, use the next free `id`, fill in at least the `en` strings, list the engines and
versions you verified it in, and credit the reporter. Translations of existing entries are welcome
too; the `de` strings in particular are mostly empty.

## License

Mozilla Public License 2.0, see `LICENSE`.
