# xbrl-rs: Parse and validate financial reports in Rust

_Published on 2026-03-28._

XBRL is an XML-based standard used in financial reporting. With
[xbrl-rs](https://github.com/quambene/xbrl-rs) you can parse _instance
documents_, and validate them against a _taxonomy_.

An instance document contains the actual report in a flat structure. For
example, to report the balance sheet of a company, the instance document
contains _facts_, like the total assets and liabilities:

``` xml
<xbrli:xbrl
    xmlns:de-gaap-ci="http://www.xbrl.de/taxonomies/de-gaap-ci-2020-04-01">
    <de-gaap-ci:bs.ass decimals="2" contextRef="I-CURRENT-YEAR" unitRef="EUR">100000.00</de-gaap-ci:bs.ass>
    <de-gaap-ci:bs.ass.currAss decimals="2" contextRef="I-CURRENT-YEAR" unitRef="EUR">80000.00</de-gaap-ci:bs.ass.currAss>
    <de-gaap-ci:bs.ass.fixAss decimals="2" contextRef="I-CURRENT-YEAR" unitRef="EUR">20000.00</de-gaap-ci:bs.ass.fixAss>
    <de-gaap-ci:bs.eqLiab decimals="2" contextRef="I-CURRENT-YEAR" unitRef="EUR">100000.00</de-gaap-ci:bs.eqLiab>
    <de-gaap-ci:bs.eqLiab.equity decimals="2" contextRef="I-CURRENT-YEAR" unitRef="EUR">50000.00</de-gaap-ci:bs.eqLiab.equity>
    <de-gaap-ci:bs.eqLiab.liab decimals="2" contextRef="I-CURRENT-YEAR" unitRef="EUR">50000.00</de-gaap-ci:bs.eqLiab.liab>
</xbrli:xbrl>
```

 In the case above, the referenced taxonomy is the Generally Accepted Accounting
 Principles (GAAP) in Germany. The taxonomy defines what can be reported and the
 relationship between these _concepts_. The concepts themselves are defined in XSD
 schema files, while the relationships are described in linkbases, which are
 simple XML files.

In the example above, the _calculation linkbase_ defines how total assets and
total liabilities are aggregated. Other linkbases include the presentation and
label linkbases. The presentation linkbase encodes the hierarchical structure of
concepts, while the label linkbase provides human-readable labels. This
structure can be used to display the facts above as a labeled tree:

| Concept          | Label                                    |      Value | Unit |
| ---------------- | ---------------------------------------- | ---------: | ---: |
| bs               | Balance sheet                            |          - |    - |
| bs.ass           | &nbsp;&nbsp;Total assets                 | 100,000.00 |  EUR |
| bs.ass.fixAss    | &nbsp;&nbsp;&nbsp;&nbsp;Fixed assets     |  20,000.00 |  EUR |
| bs.ass.currAss   | &nbsp;&nbsp;&nbsp;&nbsp;Current assets   |  80,000.00 |  EUR |
| bs.eqLiab        | &nbsp;&nbsp;Total equity and liabilities | 100,000.00 |  EUR |
| bs.eqLiab.equity | &nbsp;&nbsp;&nbsp;&nbsp;Equity           |  50,000.00 |  EUR |
| bs.eqLiab.liab   | &nbsp;&nbsp;&nbsp;&nbsp;Liabilities      |  50,000.00 |  EUR |

 The following features are supported by xbrl-rs:

- parsing XBRL instance, schema, and linkbase files
- validating an instance document against the taxonomy
- a view of the instance document

Technically, xbrl-rs uses [quick-xml](https://crates.io/crates/quick-xml) to
parse XML files. Compared to the well-known Python library
[Arelle](https://pypi.org/project/arelle-release/), there is a modest 10x
speedup in parsing large taxonomies (around 50 MB of XML files) and a 400x
speedup in validating instance documents. There is still room for performance
improvements. For example, parsing large taxonomies containing 500+ files could
be parallelized.

XBRL validation is compared against the [XBRL 2.1 conformance test
suite](https://specifications.xbrl.org/release-history-base-spec-conformance-suite.html).
Currently, xbrl-rs achieves 69% coverage

Check out the repo for more information: <https://github.com/quambene/xbrl-rs>.
