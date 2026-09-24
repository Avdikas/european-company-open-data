# ECOD - European Company Open Data

ECOD is an open, harmonised, and geocoded legal entity dataset initiative covering European Union and EFTA countries. It contributes to the development of a reproducible European data infrastructure based on official national business register data. ECOD standardises national register data into a common schema. It geocodes company addresses using offline geocoders. It publishes versioned datasets with persistent DOI records through Zenodo.

National business registers remain the authoritative source of legal entity information. ECOD does not replace, modify, or compete with official registers. It provides a transparent and reproducible harmonisation layer on top of legally accessible register data, subject to applicable national access and reuse conditions. Company registers contain information on registered legal entities. They support legal certainty, economic transparency, public administration, taxation, statistical reporting, procurement, and market analysis. ECOD focuses exclusively on registered legal entities and does not include datasets relating to natural persons.

The initiative supports the principles of open data and reuse of public sector information established by Directive (EU) 2019/1024 on open data and the reuse of public sector information. It also supports the objectives of the High-Value Datasets framework under Directive (EU) 2019/1024, including improved availability and reuse of company-related datasets where applicable.

Across Europe, company register data is often publicly available but fragmented. Data structures, formats, access methods, and reuse conditions differ between countries. This limits cross-border analysis and interoperability. ECOD addresses this challenge by creating a consistent, machine-readable, and geospatially enabled data layer. It enables comparable analysis and integration across European jurisdictions.

## Project objective

ECOD aims to produce a harmonised collection of national company datasets. The datasets are machine-readable, geocoded (latitude/longitude), versioned, reproducible, and openly reusable where legally available. All datasets preserve the provenance of the original national registers and are archived with persistent DOI identifiers through Zenodo.

The dataset supports research and academia, public administration, statistical offices, GIS and spatial analysis, economic modelling, public procurement transparency, and open governance. ECOD complements existing official and commercial data ecosystems. It provides an open and reproducible harmonisation framework based on authoritative legal entity register information.

## Current coverage

Each country is processed and published independently as a self-contained versioned dataset with its own DOI - there is no unified pan-European dataset.

**Published:**

[![ECOD Estonia](https://img.shields.io/badge/ECOD-Estonia-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.22305095)

[![ECOD Finland](https://img.shields.io/badge/ECOD-Finland-blue?style=for-the-badge&logo=zenodo)](https://zenodo.org/records/22941459)

[![ECOD Latvia](https://img.shields.io/badge/ECOD-Latvia-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.22657380)

[![ECOD Lithuania](https://img.shields.io/badge/ECOD-Lithuania-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.21259704)

## Why this project exists

Company register data across Europe is often publicly available but not available in bulk, structured inconsistently between countries, distributed in incompatible formats, and often only practically accessible through commercial aggregators or paid APIs - despite already containing high-quality official information on legal entities.

Key motivations behind ECOD are to reduce duplicated data processing effort across Europe, improve register interoperability, enable reproducible research and analytics, reduce duplicated acquisition and harmonisation efforts across organisations, and lay groundwork for future European-level statistical harmonisation.

**Long-term vision:** a standardised European company location dataset infrastructure that could support future integration with European statistical and geospatial infrastructures, as part of broader open data strategy. The scope is strictly registered legal entities and does not include datasets relating to natural persons.

## Data schema

Each ECOD dataset is delivered as a single GeoPackage (`.gpkg`) containing harmonised legal entity records and related company-level attributes from official administrative sources, organised into multiple spatial layers - one per reference year. Naming follows the convention `ECOD_{CountryCode}_{Version}.gpkg` (e.g. `ECOD_LT_v1.gpkg`), with internal layers named `ECOD_{CountryCode}_{Year}` (e.g. `ECOD_LT_2018`, `ECOD_LT_2019`, ...).

Each yearly layer contains harmonised company data for that reference year and preserves historical continuity with prior years - i.e., the GeoPackage for a given year includes that year's layer plus all previous available years. Attributes may vary between years depending on data availability, reporting requirements, legal changes, and what the national source provides.

**Mandatory fields:**

| Field | Description |
|---|---|
| `countryId` | ISO Alpha-2 country code (NUTS-0 equivalent) |
| `companyId` | National company identifier |
| `legalName` | Registered company name, local language |
| `companyType` | Legal form (LLC, partnership, etc.), local language |
| `status` | Company status (active, inactive, bankrupt, dissolved, or national equivalent) |
| `vatNumber` | VAT identification number, where available |
| `foundationDate` | Company establishment date |
| `address` | Registered postal address (city, street, building number, postcode) |
| `employees` | Average reported employee count for the year, where available |
| `turnover` | Annual turnover/revenue, where available (EUR or local currency) |
| `naceCode` | Economic activity classification (NACE version applicable to that year) |

**Optional fields (generated during processing):**

| Field | Description |
|---|---|
| `latitude` | Latitude from geocoding |
| `longitude` | Longitude from geocoding |
| `accuracy` | Geocoding quality/reliability indicator |

## Data contribution

Contributions are welcomed from national business registers, taxation authorities, labour and employment registers, statistical offices, government open data portals, public sector institutions, and research organisations. Source datasets may provide legal entity records or additional company-level attributes, such as employment, financial, or classification information, where legally available. All contributions remain fully attributed to the original data provider.

**Supported input formats:** GeoPackage, structured CSV exports, PostgreSQL/PostGIS, and ArcGIS File Geodatabase.

## How contribution works

1. **Provide dataset** - A contributing organisation supplies a company register extract. Existing coordinates are preserved; geocoding is applied only where coordinates are missing.
2. **Processing** - Schema harmonisation, address normalisation, geocoding (if required), data validation, coordinate quality control, metadata generation, and versioning.
3. **Geocoding (if required)** - Performed using [Open ArcGIS Pro Offline Locators](https://github.com/Avdikas/open-arcgis-pro-offline-locators). Skipped if coordinates already exist.
4. **Publication** - Final GeoPackages are published on Zenodo with a DOI, version number, full metadata, and source attribution.
5. **Access** - Datasets are publicly accessible on Zenodo: harmonised outputs, geocoded data, historical versions, and metadata.

## Workflow overview

A reproducible geospatial ETL pipeline:

1. **Data ingestion** - official national registers obtained from authorities or open data portals
2. **Schema harmonisation** - transformation into the common ECOD schema
3. **Address normalisation** - address cleaning and standardisation
4. **Geocoding** - offline locator-based geocoding, where required
5. **Quality assurance** - duplicate, coordinate, and schema-consistency validation
6. **Dataset assembly** - construction of the harmonised national dataset
7. **Zenodo publication** - archival with DOI and version history

## Geocoding system

Geocoding uses [Open ArcGIS Pro Offline Locators](https://github.com/Avdikas/open-arcgis-pro-offline-locators), chosen for offline processing, reproducibility, multilingual address support, consistent cross-country matching, and independence from external APIs or commercial geocoding services.

## Publication model

Each dataset is published through Zenodo (DOI archival) with documentation maintained on GitHub. Every country dataset carries its own release history, versioning, and citation metadata. Each dataset records the original data source, acquisition date, processing steps, transformations, and publication version. ECOD does not alter the legal meaning of source records. All harmonised fields remain traceable to the originating register.

## FAIR principles

ECOD is built around the FAIR principles - Findable, Accessible, Interoperable, Reusable.

## Why contribute

Many European countries maintain high-quality, publicly accessible or open-licensed company registers, yet reuse is limited by fragmented systems, inconsistent formats, absent harmonised schemas, missing spatial coordinates, and duplicated effort across independent users. ECOD addresses this by harmonising official sources, improving interoperability, enabling geospatial analytics, cutting redundant commercial data acquisition, and supporting open research and public-sector analytics - moving toward a European ecosystem where harmonised company data is a standard part of statistical and geospatial infrastructure.

## Technical notes

- Fully reproducible ETL pipeline
- Geocoding step is optional (applied only when coordinates are missing)
- Version-controlled transformations with complete provenance tracking
- Every dataset ships with metadata and source attribution

## License

- **Repository documentation:** MIT License
- **Data:** Retains original source licenses; attribution to original providers is mandatory

## Disclaimer

National business registers remain the authoritative source. ECOD makes no legal modifications to source data. Geocoded coordinates are estimates dependent on address quality, and overall data quality depends on the original source. ECOD does not guarantee completeness or continuous availability of national source data. No liability is assumed for analytical use.

## Maintainer

**UAB Demolit** (Lithuania) - data infrastructure and open data initiative focused on harmonised European company datasets
📧 opendata@demolit.lt

## Author

© Andrius Kučas, 2026
