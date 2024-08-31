<!-- markdownlint-disable MD001 -->

# LibreCRM Release v0.1.0: Open source customer relationship management based on LibreOffice

_First published on [Reddit](https://www.reddit.com/r/libreoffice/comments/uekl2v/librecrm_v010_open_source_customer_relationship/) (2022-04-29)._

I was using a simple spreadsheet (LibreOffice Calc) for my own projects.
However, spreadsheets inevitably become kind of messy over time, so I re-wrote
the spreadsheet in LibreOffice Base.

[LibreCRM](https://github.com/quambene/libre_crm) is an open-source customer
relationship management (CRM) system based on LibreOffice.

### The workflow

 The simple workflow is based on the following 6-state lead status:

- Todo
- Doing - cold
- Doing - warm
- Doing - hot
- Done - closed
- Done - rejected

The status _Doing_ is subdivided into cold, warm, and hot leads which
corresponds to

- information qualified lead,
- marketing qualified lead, and
- sales qualified lead

in sales terminology.

The workflow is either finished with a success (_Done - closed_) or failure
(_Done - rejected_).

### The source code

You can find the source code (extracted from the `odb` file) and the `odb` file
itself in the Github repository.

Building the `odb` from source ensures repoducible builds and prevents possible
corruption of the `odb` file. This way LibreCRM can be improved continuously.

Check out the repo for more information: <https://github.com/quambene/libre_crm>.
