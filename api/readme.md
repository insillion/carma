# Carma Cannabis Insurance Quote API – Integration Guide

**Version:** v1.0  
**Prepared By:** Insillion  
**Prepared For:** Carma Insurance
**Last Updated:** 23-Dec-2025  

---

## 1. Introduction

This document provides detailed technical information for **Carma Quote API**.

The API collection enables authorized partners to authenticate, calculate insurance premium, create, update and finalize quote. Post finalization, it can be assigned to UW. 

**Intended Audience:**
- Integration partners
- Technical architects

---

## 2. Environment Details

### Production Environment
**Base URL:**  
`To be updated`

### Sandbox Environment  
`https://carma.sb.insillion.com`

------

## 4. API Workflow (High-Level)

### 4.1 Recommended Integration Flow
1. Generate Authentication Token  
2. (Optional) Calculate Premium  
3. Create New Quote  
4. Update / Save Quote  
5. Finalize Quote  
6. Assign Quote to Underwriter  
7. View Quote Details  

---

## 4.2 Common Quote Request Structure

Used by:
- Premium Calculation API
- Create Quote API
- Update Quote API

## Parent-Child Location Rule (Very Important)

For all child arrays (`cultivator_info`, `manufacturing_info`):

- `loc_no` and `building_no` **must match** the corresponding values in `operation_type`
- If mismatch occurs → **validation error** will be returned

---

## Request Schema

### customer_details (object)

| Field | Type | Required |
|------|------|----------|
| gnrlinfo_company_name | string | Yes |
| gnrlinfo_applicant_contact_name | string | No |
| gnrlinfo_legal_business_name | string | Yes |
| gnrlinfo_mailing_address | string | No |
| email | string | Yes |
| gnrlinfo_fein_number | string | Yes |
| gnrlinfo_zip_code | string | No |
| gnrlinfo_phone_number | string | Yes |

---

## General Fields

| Field | Type | Required | Condition |
|------|------|----------|-----------|
| gnrlinfo_commercial_general_liability | string | Conditional | At least one liability coverage must be `"Yes"` |
| gnrlinfo_product_liability | string | Conditional | At least one liability coverage must be `"Yes"` |
| gnrlinfo_commercial_property | string | Conditional | At least one liability coverage must be `"Yes"` |
| gnrlinfo_excess_liability | string | Conditional | At least one liability coverage must be `"Yes"` |
| gnrlinfo_new_venture | string | Yes | |
| gnrlinfo_license_status | string | Yes | |
| gnrlinfo_year_established | string | Yes | |
| policy_start_date | string | No | |
| gnrlinfo_have_previous_insurance | string | Yes | |
| gnrl_info_additional_comments_or_questions | string | No | |

---

## operation_type (array)

| Field | Type | Required |
|------|------|----------|
| liability_loc_no | string | Yes |
| liability_buildingno | string | Yes |
| optype | string | Yes |
| op_projected_ny_salesrevenue | number | Yes |

---

## Conditional Arrays

### cpi_location_details (array – conditional)

**Required when:** `gnrlinfo_commercial_property = "Yes"`

| Field | Type | Required |
|------|------|----------|
| cpi_loc_no | string | Yes |
| cpi_building_no | string | Yes |
| cpi_locwise_optype | string | Yes |
| cpi_construction_type | string | Yes |

---

### cpi_coverage_details (array – conditional)

**Required when:** `gnrlinfo_commercial_property = "Yes"`

| Field | Type | Required |
|------|------|----------|
| cpi_cd_locno | string | Yes |
| cpi_cd_bdno | string | Yes |
| cpi_cd_coverages | string | Yes |
| cpi_cd_cover_opted | string | Yes |
| cpi_cd_suminsured | number | Yes |

---

### cultivator_info (array – conditional)

**Required when:** `operation_type.optype = "Cultivator for commercial sale"`

| Field | Type | Required |
|------|------|----------|
| cinfo_loc_no | string | Yes |
| cinfo_build_no | string | Yes |
| gnrlinfo_type_of_growlight | string | Yes |
| gnrlinfo_how_often_growlight_replace | string | Yes |
| gnrlinfo_warrant | string | Yes |

---

### manufacturing_info (array – conditional)

**Allowed only when:**  
`operation_type.optype = "Cannabis Products Manufacturing w/o solvent"`  
**OR**  
`operation_type.optype = "Cannabis Manufacturer - Processor w/solvent"`

| Field | Type | Required |
|------|------|----------|
| manfinfo_loc_no | string | No |
| manfinfo_build_no | string | No |
| grnl_info_extraction_method | string | No |
| grnl_info_other_extraction_method | string | No |
| gnrl_info_is_closedloop_extraction | string | No |
| gnrl_info_c1d1room | string | No |
| gnrl_info_non_extraction_process | string | No |

---

All APIs follow REST standards and communicate using **JSON**.

### Brokers
|# | API | Description |
|:--:|:--:|:--|
|1|[Auth](./broker/01-auth.md)| Authentication Request & Response|
|2|[PREMIUM CALC](./broker/02-premium-calc.md)| Premium Calc Request & Response|
|3|[Quote-Create](./broker/03-quote-create.md)| Quote Create Request & Response|
|4|[Quote Update / Save ](./broker/04-quote-update-save.md)| View Quote Update / Save  Request & Response|
|5|[Quote Finalize](./broker/05-quote-finalize.md)| View Quote Finalize Request & Response|
|6|[Quote Assign To UW](./broker/06-quote-assign-To-UW.md)| Quote Assign To UW Request & Response|
|7|[View Quote](./broker/07-view-quote.md)| View Quote Request & Response|

