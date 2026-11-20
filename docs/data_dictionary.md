
# Data Dictionary

## Project Overview

This document describes the source dataset fields, their corresponding analysis fields, and the data preparation performed in the Zomato Bengaluru Restaurant Analysis project.

The source CSV schema may vary depending on the dataset version.

## 1. Source-to-Analysis Field Mapping

| Source field | Analysis field | Description |
|---|---|---|
| `name` | `name` | Restaurant/listing name |
| `location` | `location` | Neighbourhood or locality |
| `rate` | `rating` | User rating, converted to a numeric scale out of 5 |
| `approx_cost(for two people)` | `cost_for_two` | Approximate cost for two, converted to numeric |
| `votes` | `votes` | Recorded vote count |
| `online_order` | `online_order` | Online-order availability: Yes/No/Unknown |
| `book_table` | `book_table` | Table-booking availability: Yes/No/Unknown |
| `rest_type` | `rest_type` | Restaurant format/type |
| `cuisines` | `cuisines` | Comma-separated cuisine tags |

## 2. Data Preparation and Transformations

The notebook performs the following preparation steps:

### Rating
- Converts rating values from text into numeric values.
- Converts values such as `4.1/5` into `4.1`.
- Treats invalid entries such as `NEW` and `-` as missing.
- Treats ratings outside the valid 0–5 range as missing.

### Approximate Cost
- Removes commas from cost values.
- Converts the column into numeric format.
- Treats invalid and negative values as missing.

### Votes
- Converts vote counts into numeric values.
- Treats invalid and negative values as missing.

### Online Ordering and Table Booking
- Standardises values into three categories: Yes, No and Unknown.
- Missing or unrecognised entries are represented as Unknown.

### Cuisine Data
- Separates multiple cuisines listed in a single record into individual tags.
- Expands cuisine tags for cuisine-level analysis.

### Duplicate Records
- Identifies duplicate records using the retained analytical columns.
- Removes duplicate rows during data preparation.

## 3. Missing Data Handling

- Missing ratings and cost values are retained in the cleaned dataset.
- Individual analyses use only the available values required for their calculations.
- Unknown service availability is kept separate from confirmed Yes and No responses.

## 4. Columns Excluded from Analysis

The following original fields are excluded from the main analytical dataset:

- `url`
- `address`
- `phone`
- `reviews_list`
- `menu_item`
- `dish_liked`
- `listed_in(type)`
- `listed_in(city)`

These fields are outside the selected analysis scope.

## 5. Data Limitations

- The dataset represents a historical snapshot and may not reflect the current restaurant landscape.
- Restaurant ratings, costs and service availability may have changed since collection.
- Missing and inconsistent values may affect individual analyses.
- Observed relationships between variables do not establish causation.
