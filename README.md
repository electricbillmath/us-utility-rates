# U.S. electric utility residential rates 2025

Average residential electricity price, usage and bill for every U.S. electric utility that reports residential sales, every Texas retail provider and the six Texas delivery utilities, one row per utility and state. Built from the EIA Form 861 annual survey (data year 2025) and cleaned for direct use: readable names, a comparability flag and links to an explanation page for each larger utility.

- **1,510 rows**, all 50 states + DC
- 1,328 `utility`, 62 `retail_provider`, 6 `tx_delivery_utility`, 114 `behind_the_meter_solar`
- Files: [`data/electricbillmath-utilities-2025.csv`](data/electricbillmath-utilities-2025.csv) (CSV, UTF-8) and [`data/electricbillmath-utilities-2025.json`](data/electricbillmath-utilities-2025.json) (JSON)
- Browse it: [electricbillmath.com](https://electricbillmath.com/) · [average electric bill by state](https://electricbillmath.com/average-electric-bill/) · [methodology](https://electricbillmath.com/methodology/)

## Columns

| Column | Type | Description |
|---|---|---|
| `eia_id` | integer | EIA utility number (Form 861). Stable across years; join key for other EIA data. |
| `state` | string | Two-letter state code (incl. DC). A utility serving several states has one row per state. |
| `name_eia` | string | Name exactly as reported to EIA. |
| `name_common` | string | Name customers know (e.g. "Pacific Gas & Electric" for "Pacific Gas & Electric Co."). For Texas holding companies the retail brands are added, taken from the PUCT REP directory. |
| `ownership` | string | EIA ownership class: Investor Owned, Cooperative, Municipal, Political Subdivision, State, Federal, Retail Power Marketer, Behind the Meter. Empty for Texas delivery utilities. |
| `type` | string | utility = sells energy and delivery together; retail_provider = competitive retailer (mainly Texas); behind_the_meter_solar = rooftop solar lease/PPA company; tx_delivery_utility = Texas wires company (TDU). |
| `residential_customers` | integer | Residential customers (annual average) for bundled or retail service. |
| `avg_cents_per_kwh` | number | Residential revenue divided by residential sales, in cents per kWh. All-in average, including fixed charges. |
| `avg_kwh_per_month` | integer | Residential sales per customer per month, in kWh. |
| `avg_bill_usd_per_month` | number | Residential revenue per customer per month, in US dollars. |
| `delivery_only_customers` | integer | Customers that buy only delivery from this utility (energy from a competitive supplier). Empty where not reported. |
| `delivery_cents_per_kwh` | number | Delivery revenue divided by delivery sales for those customers, in cents per kWh. |
| `comparable` | string | no = should not be ranked against utilities: solar lease/PPA companies, and Texas retail providers below 12 cents/kWh whose reported revenue does not cover a full bill. |
| `page_url` | string | Page on electricbillmath.com with the explanation for this utility. Empty for small utilities without a page. |

## Things to know before you use it

- **These are averages, not tariffs.** `avg_cents_per_kwh` is total residential revenue divided by kWh sold, so fixed monthly charges and riders are included. It is the price customers actually paid on average in 2025, not the rate on a tariff sheet.
- **Deregulated states.** Where customers can choose a supplier, the utility reports delivery-only customers separately (`delivery_only_customers`, `delivery_cents_per_kwh`). The energy part is reported by the retail providers.
- **Texas.** Most of Texas has no bundled utility. Retail providers report their own revenue; some report figures below 12 ¢/kWh that cannot be a full bill. Those rows are marked `comparable = no`. The six Texas delivery utilities (Oncor, CenterPoint, AEP Texas Central/North, TNMP, Lubbock P&L) are included as `tx_delivery_utility` from EIA's Delivery Companies table. Current 2026 delivery tariffs are on [electricbillmath.com/texas-delivery-charges/](https://electricbillmath.com/texas-delivery-charges/).
- **Solar leases and PPAs** (Tesla, Sunrun, SunPower Capital and others) report as "Behind the Meter". They are kept as `behind_the_meter_solar` with `comparable = no`, because they do not supply a whole household.
- **What is left out.** Rows EIA marks as adjustments, rows without residential customers, and figures outside 3 to 80 cents/kWh (reporting errors). Energy-only suppliers outside Texas (EIA Part B) are not listed one by one.
- **Names.** `name_eia` is unchanged. `name_common` only changes display names; nothing is merged or dropped.

## Sources

- U.S. Energy Information Administration, [Form EIA-861 annual electric power industry report](https://www.eia.gov/electricity/data/eia861/), data year 2025: tables Sales to Ultimate Customers and Delivery Companies. Public domain.
- Public Utility Commission of Texas, REP directory: brand names of Texas retail providers.
- Open Energy Data Initiative (OEDI), NREL: "U.S. Electric Utility Companies and Rates: Look-up by Zip Code", CC BY 4.0. Used on the website for ZIP lookups; not part of this file.

## License and citation

[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may copy, adapt and use the data commercially. Please cite:

> Electric Bill Math (electricbillmath.com), utility electricity rates 2025, based on EIA Form 861 and OEDI ZIP-to-utility data. CC BY 4.0.

A [CITATION.cff](CITATION.cff) file is included; GitHub shows a "Cite this repository" button for it.

## Updates

EIA publishes the final Form 861 data about ten months after the data year ends. This repository is updated once a year when it does. Corrections: open an issue or write to contact@electricbillmath.com.
