# Document Buffet V1

Link to try: [Document Buffet
](https://testingtours.github.io/mymzt/document-buffet.html)
## Quick Start

Open `index.html` locally, or publish this repository with GitHub Pages from the repository root. The default Pages URL will load the builder directly.

Required static files:

- `index.html` - GitHub Pages entry point
- `document-buffet.html` - named copy of the same builder
- `pages/cover.html` - standalone cover template
- `assets/mzt/` - required logo, font, and image assets
- `.nojekyll` - prevents GitHub Pages from processing the static files

## How URL Parameters Work

Any visible sidebar field can be prefilled by using its HTML `id` as a query parameter.

The app also updates the browser URL as you edit fields, upload images, toggle pages/sections, and reorder pages. Copy the current address bar URL to share the current book setup.

Example:

```text
index.html?coverTitle=The%20Benelux%20Tour
```

Long text should be passed as normal URL-encoded text. Use Markdown-style formatting inside large text fields.

```text
index.html?day4ItineraryBody=This%20is%20%2A%2Abold%2A%2A%20and%20this%20is%20%2Aitalic%2A.%0A%0A-%20First%20bullet%0A-%20Second%20bullet
```

For line breaks in normal query parameters, use `%0A`.

```text
index.html?contactDetails=Mile%20Zero%20Tours%3A%0A208-620%20View%20Street
```

Images can be set using regular direct URLs or base64 `data:` URLs. For data URLs, URL-encode the whole value so characters like `+`, `/`, `=`, and `&` do not break the query string.

```text
index.html?coverHeroSrc=https%3A%2F%2Fexample.com%2Fimage.jpg
```

```text
index.html?coverHeroSrc=data%3Aimage%2Fpng%3Bbase64%2CiVBORw0KGgo...
```

The old `_b64` parameter fallback still exists, but Markdown text with URL encoding is the preferred format for text content.

## Markdown In Large Text Fields

Large body fields support a small Markdown-style subset:

| Syntax | Result |
|---|---|
| `**bold**` | Bold text |
| `*italic*` | Italic text |
| `[label](https://example.com)` | Link |
| Blank line | New paragraph |
| `- item` or `* item` | Bullet list |

HTML is escaped before Markdown formatting is applied.

## Page Toggles

Turn one page on or off:

```text
index.html?page.airport-security=false
```

Use a strict list of pages to include:

```text
index.html?pages=cover,services,airport-security,daybyday-l1
```

Set page order:

```text
index.html?order=cover,services,airport-security,daybyday-l1,things-to-remember,notes
```

The app writes `order=` automatically when pages are moved with the arrow buttons.

Boolean values accepted as false:

```text
0, false, off, no, unchecked
```

Everything else is treated as true.

## Section Toggles

Turn individual subsections on or off:

```text
index.html?section.things-to-remember.things-luggage=false
```

Format:

```text
section.{pageId}.{sectionId}=true-or-false
```

## Pages And Sections

| Page name | Page ID | Default | Sections |
|---|---|---:|---|
| Cover | `cover` | On | `cover-layout` |
| Personal Details | `services` | On | `services-summary` |
| Airport Security | `airport-security` | On | `airport-wear`, `airport-pack`, `airport-cannabis` |
| DayByDay-L1 | `daybyday-l1` | On | `daybyday-l1-image`, `daybyday-l1-summary` |
| DayByDay-L2 | `daybyday-l2` | On | `day-by-day-main-image`, `day-by-day-days` |
| DayByDay-L3 | `daybyday-l3` | On | `day-by-day-main-image`, `day-by-day-days` |
| DayByDay-Bland | `daybyday-bland` | On | `daybyday-bland-days` |
| Things To Remember | `things-to-remember` | On | `things-hotels`, `things-luggage`, `things-contact` |
| Reminder Details | `remember-details` | On | `remember-detail-sections` |
| Notes | `notes` | On | `notes-box` |

## Image Parameters

These parameters update image sources directly:

| Parameter | Affects |
|---|---|
| `coverLogoSrc` | Cover page logo |
| `coverHeroSrc` | Cover page main image |
| `dayStyle1ImageSrc` | DayByDay-L1 image |
| `dayByDayMainImageSrc` | DayByDay-L2/L3 top image |
| `day2ImageSrc` | DayByDay-L2/L3 inline image |

Each image parameter accepts either a direct URL or a URL-encoded base64 data URL.

## Field Parameters

### Cover

| Field ID | Purpose |
|---|---|
| `coverTitle` | Tour title |
| `coverDates` | Tour date range |
| `coverGuideType` | Document type, such as Travel Guide |
| `coverPreparedFor` | Guest name |
| `coverBooking` | Booking number |

Upload controls are not URL-prefilled directly. Use image parameters instead:

- `coverLogoSrc`
- `coverHeroSrc`

### Personal Details

| Field ID | Format |
|---|---|
| `servicesWelcome` | Plain text |
| `servicesThanks` | Plain text |
| `servicesIntro` | Plain text |
| `pickupFrom` | Plain text |
| `pickupConfirm` | Plain text |
| `pickupNote` | Plain text |
| `flightAirline` | Plain text |
| `departureFlights` | Multi-line. First line is date/header, following rows use `Flight | Time | Route` |
| `returnFlights` | Multi-line. First line is date/header, following rows use `Flight | Time | Route` |
| `hotelRows` | Multi-line rows using `Nights | Hotel name/location` |
| `mealRows` | Multi-line rows using `Meal | Details` |
| `additionalRows` | One inclusion per line |

Example with line breaks:

```text
departureFlights=Thursday%2C%20April%2016%2C%202026%0AAC%201902%20%7C%2011%3A30%20am%20-%207%3A12%20pm%20%7C%20Victoria%20to%20Toronto
```

### Airport Security

| Field ID | Format |
|---|---|
| `airportTitle` | Page title |
| `airportWearTitle` | First section heading |
| `airportWearIntro` | Paragraph text |
| `airportWearBullets` | One bullet per line |
| `airportWearBody` | Paragraphs separated by blank lines |
| `airportPackTitle` | Second section heading |
| `airportPackIntro` | Paragraph text |
| `airportPackBullets` | One bullet per line |
| `airportCannabisTitle` | Third section heading |
| `airportCannabisBody` | Paragraph text |

### DayByDay-L1

This layout is the single image plus summary page.

| Field ID | Purpose |
|---|---|
| `dayStyle1Heading` | Green summary heading |
| `dayStyle1Summary` | Summary paragraphs separated by blank lines |

Image:

- `dayStyle1ImageSrc`

### DayByDay-L2 And DayByDay-L3

These layouts use the same fields. L2 floats the inline image left. L3 floats the inline image right.

| Field ID | Purpose |
|---|---|
| `dayByDayTitle` | Section title |
| `dayByDayMainImageEnabled` | Checkbox: show/hide top image |
| `day2ImageEnabled` | Checkbox: show/hide Day 2 inline image |
| `day1ItineraryTitle` through `day13ItineraryTitle` | Day headings |
| `day1ItineraryBody` through `day13ItineraryBody` | Day body copy |

Images:

- `dayByDayMainImageSrc`
- `day2ImageSrc`

Example:

```text
index.html?dayByDayMainImageEnabled=false&day2ImageEnabled=true
```

### DayByDay-Bland

Text-only day-by-day layout.

| Field ID | Format |
|---|---|
| `blandDayRows` | Blocks separated by a blank line. First line is the day heading; following lines are body text. |

Example block:

```text
DAY 7 - WEDNESDAY APRIL 23, 2025 - ANTWERP TO BRUGES
Body copy goes here.
Today's breakfast is included.
```

### Things To Remember

| Field ID | Format |
|---|---|
| `hotelContactRows` | One hotel per line: `Date | Hotel | Address | Phone` |
| `luggageRows` | One row per line: `Label | Details` |
| `contactIntro` | Paragraph text |
| `contactDetails` | One contact-card line per line |

### Reminder Details

| Field ID | Format |
|---|---|
| `rememberDetailRows` | One section per line: `Heading | Body text` |

### Notes

The notes page has no text fields. It renders a blank bordered notes box.

### Custom Page Controls

These are for interactive use only and are not intended as stable URL parameters:

| Field ID | Purpose |
|---|---|
| `customPageTitle` | New custom page title |
| `customHeading` | New custom section heading |
| `customBody` | New custom section body |
| `customTargetPage` | Select target page for a custom section |

## Practical Examples

Only show the cover and personal details pages:

```text
index.html?pages=cover,services
```

Open a custom page order:

```text
index.html?order=cover,services,airport-security,daybyday-l1,notes
```

Set guest and booking:

```text
index.html?coverPreparedFor=Jane%20Smith&coverBooking=MZT-12345
```

Hide the airport page for a bus or boat tour:

```text
index.html?page.airport-security=false
```

Hide only the luggage subsection:

```text
index.html?section.things-to-remember.things-luggage=false
```

Prefill Day 4 title:

```text
index.html?day4ItineraryTitle=Day%204%20-%20Rotterdam
```

Use Markdown for long Day 4 copy:

```text
index.html?day4ItineraryBody=Today%20we%20visit%20%2A%2ARotterdam%2A%2A.%0A%0A-%20Market%20visit%0A-%20Free%20time
```

Set a cover image by URL:

```text
index.html?coverHeroSrc=https%3A%2F%2Fexample.com%2Fcover.jpg
```

## Updating GitHub Pages

After changing files locally:

1. Commit `index.html`, `document-buffet.html`, `pages/`, `assets/`, `.nojekyll`, and `README.md`.
2. Push to GitHub.
3. In GitHub repository settings, enable Pages from the repository root.

No build step is required.
