# accessible-books-in-browsers

[Github project page](https://github.com/daisy/accessible-books-in-browsers)

## About 

Transform EPUB with Media Overlays into a series of HTML files for reading directly in the browser. 

A typical conversion creates the following files (see an [example fileset](https://github.com/daisy/accessible-books-in-browsers/tree/main/demos/moby-dick)):
- HTML files with the original contents, plus reading interface controls and links to the TOC, Previous, and Next pages.
- An About page containing publication metainformation
- A TOC based on the original EPUB Nav Document

Media Overlays conversion adds the following:
- Creation of one audio file per HTML page
- Embedding that audio file in the HTML page
- A VTT file containing the phrase timing information for that audio file

## Demos

* [Action for Heroes](https://daisy.github.io/accessible-books-in-browsers/demos/action-for-heroes)
* [Moby Dick](https://daisy.github.io/accessible-books-in-browsers/demos/moby-dick)

These demos were created using this [conversion script](https://github.com/daisy/accessible-books-in-browsers/tree/main/convert). 


## Current features

| Feature | Basic | JS-enhanced |
|---------|-------|-------------|
| Spine navigation | Forward and back through the spine documents with links (shown as arrows) | (same) | 
| TOC | TOC link opens `nav.html`| TOC loads in sidebar | 
| Page list | Page list is within `nav.html`, use landmarks navigation or click the in-page link at top | Page list loads in sidebar and has go-to-page controls | 
| Search | Not available | Full text search available from sidebar |
| Publication info | Info link opens `about.html`, containing publication info | About page loads in sidebar instead|
| Keyboard shortcuts | Not available | Available (see help for details) | 
| Help | Opens in new page | (same) |
| Settings | Not available | Change size, theme, playback rate, page number announcements |
| Theme | Match OS dark theme preference by default | Adds ability to turn on/off |
| Bookmarks | Bookmark any heading using your browser | (same) |
| Audio support | Play embedded audio for the page with native HTML controls | Adds synchronized highlighting and custom controls, including phrase navigation and control over announcing page numbers|


## Caveats

### Conversion
A few things (navigation document consistency across publications; colors in stylesheets or things marked `!important`) were adjusted manually in the EPUB source; this is, after all, just a prototype. But these aspects can and will be automated in the future.


### User interface

- Autoplay between chapters is [not working yet](https://github.com/daisy/accessible-books-in-browsers/issues/3)
- Slight flashing on page load if not using dark mode

[See issues list](https://github.com/daisy/accessible-books-in-browsers/issues)

## Approach

Generate a set of HTML pages:
* Target DAISY 2.02 content which has been automatically converted to EPUB 3
* Use an HTML template prepopulated with the basic structure of our pages (intra-publication links, audio if applicable)
* For each EPUB HTML spine item (except for the TOC), move the contents of `<body>` into the HTML template's `<main>` element.
* Generate a navigation file based on the EPUB navigation document
* Generate an About file containing publication information
* The cover page is renamed `index.html` and can act as an entry page (though a user can enter the publication from any page)
* Add links to each heading for easy bookmarking

Add javascript enhancements:
* Sidebar with table of contents, page list, search, and about tabs
* Settings panel to control visual adjustments and audio preferences
* Audio playback with synchronized highlighting
* Keyboard shortcuts

What this isn't:
* An authoring format definition
* A generic "player" to apply to any EPUB
