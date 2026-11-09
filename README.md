# ekiotools

ekiotools collects the tools EKIO uses to publish its work. It currently builds LinkedIn document carousels for package announcements and exports them to HTML, PDF, and PNG.

## Installation

```r
# install.packages("pak")
pak::pak("viniciusoike/ekiotools")
```

PDF and PNG export use Chrome through the chromote package:

```r
install.packages(c("chromote", "jsonlite"))
```

## Example

```r
library(ekiotools)

brand <- promo_brand(
  package = "trendseries",
  version = "1.7.0",
  logo = "man/figures/logo.png",
  docs_url = "https://viniciusoike.github.io/trendseries/"
)

cards <- list(
  promo_cover("trendseries 1.7.0", "Trend extraction for economic time series"),
  promo_feature(
    "Rebase series to a common index",
    code = "# rebase to 2020 = 100\nrebase(series, base = 2020)",
    badge = "New"
  ),
  promo_closing("Try it today")
)

render_promo(cards, brand, "promo/carousel.html", png_dir = "promo/pages")
```

`render_promo()` writes a self-contained HTML file and a 1080 × 1350 PDF. With `png_dir`, it also writes one PNG per page. Export stops when a card overflows its page, so shorten that card instead of shrinking the text.

Install the fonts you configure in `promo_brand()` locally. The carousel requests no web fonts.
