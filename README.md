# Get Lighthouse scores for multiple URLs

This app takes URLs and optional metadata from [_input.csv_](src/input.csv) (one row per URL), runs one or more audits synchronously, and outputs median scores to [_output.csv_](src/output.csv).

You can specify multiple different options using the flags below.

For example:

- The number of times Lighthouse tests each URL. The default is three.
- Whether to calculate the average or median scores for all the runs. The default is median.
- Which Lighthouse audits to run. The default is all audits: Performance, Best practice, PWA, Accessibility, SEO.

---

## Installation and usage

1. Clone the code using git: `git clone git@github.com:samdutton/multihouse.git` or [download it as a ZIP file](https://github.com/samdutton/multihouse/archive/master.zip).
2. From a terminal window, go to to the `multihouse` directory you created and run `npm install` to install the required Node modules.
3. Add URLs to be audited (and optional metadata) to [_input.csv_](src/input.csv), as described below.
4. From a terminal `cd` to the `src` directory and run `node index.js`, optionally setting the flags below.
5. Progress updates and errors will be logged to the console.
6. When all Lighthouse runs are complete, view the results in [_output.csv_](src/output.csv).
7. Check for errors in _error-log.txt_.

## Input and output data format

Each line in [_input.csv_](src/input.csv) begins with a URL, optionally followed by other comma-separated data for the URL.

For example:
```
  My site,homepage,https://example.com
```
Results are written to [_output.csv_](src/output.csv) with one line per URL. For example:

```
  My site,homepage,https://example.com,0.50,0.38,0.78,0.87,1
```
_input.csv_ and _output.csv_ in this repo both include real example data.

## Error handling

- Lighthouse runtime errors are logged in _error-log.txt_.
- Any audit that returns a zero score is disregarded, and a warning for the URL and score is logged in _error-log.txt_.
- URLs with Lighthouse errors are not included in output data.


## Command line options

```
-a, --append        Append output to existing data in output file
-c, --categories    Audits to run: one or more comma-separated values,
                    default is:
                    performance,pwa,best-practices,accessibility,seo
-f, --flags         One or more comma-separated Chrome flags without dashes,
                    default is --headless
-h, --help          Show help
-i, --input         Input file, default is input.csv
-m, --metadata      Optional column headings to be used as the first row of
                    _output.csv_, for example: Page, Type, Performance, SEO
-o, --output        Output file, default is output.csv
-r, --runs          Number of times audits are run to calculate median scores,
                    default is 3
-s, --score-method  Method of score aggregation, default is median
```

##  More

- It's straightforward to log the complete Lighthouse report for each run. By default only aggregate audit scores are recorded. Look for the code in [`index.js`](src/index.js) marked `***`.
- The data from [`output.csv`](src/output.csv) can easily be used to automatically update a spreadsheet and produce charts using an application such as Google Sheets.
- See [`TODO`](TODO) for work in progress.


---

Please note that this is not an official Google product.

