# Introduction

## Purpose

The purpose of this document is to describe the physical design of the configuration entities in the Ecoation Backend. This document only describes new configuration entities as designed to be part of the next development iteration starting at Jan 7, 2019.

## Scope

The configuration entities described in this document are used by these teams in Ecoation Innovative Systems Inc. :

* Firmware

* Back-end

* Data-science

## Notes

*Notes. guidelines, maps, …*

## References

* REF#1: Configuration Entities - Logical Design

    * [https://docs.google.com/document/d/1v3hAZVxyyfT2v5bvpBT0LsZDmQ1VLq6jZSd62FvA5_g/edit?usp=sharing](https://docs.google.com/document/d/1v3hAZVxyyfT2v5bvpBT0LsZDmQ1VLq6jZSd62FvA5_g/edit?usp=sharing)

* REF#2: Best Practices for DynamoDB

    * [https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

# Design Characteristics

## Physical Environment

The entities designed in REF#1 are implemented as tables in DynamoDB on Amazon Web Services (AWS). 

## Design Guideline

We almost followed NoSQL design patterns and best practices for DynamoDB as described by AWS documentation:

* [https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

## Abbreviations

Keys:

* PK: Partition Key

* SK: Sort Key

Data types:

* S: String

* N: Number

* B: Boolean

* L: List

* M: Map

# Tables

## b-c-config

This table contains almost all "basic" configuration entities according to REF#1. It is arranged in such a way that each configuration category/entity can be retrieved easily and independently. The following entities from REF#1 are packed into this table:

* Sys Config

* Crop Variety

* Label

 

### Table design

<table>
  <tr>
    <td>Primary Key</td>
    <td></td>
    <td>

Attributes</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>config_type (PK) (S)</td>
    <td>config_key 
(SK) (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>

sys</td>
    <td>config_version</td>
    <td>crops (L)</td>
    <td>label_categories (L)</td>
    <td>machine_types (L) </td>
    <td></td>
    <td>account_types (L)</td>
  </tr>
  <tr>
    <td></td>
    <td>latest#sys#{date}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>config_version</td>
    <td>pulse_lights (L)</td>
    <td>solid_lights (L)</td>
    <td>aux_sensors (L)</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>latest#recipe#{date}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
crop_variety</td>
    <td>crop_variety</td>
    <td>crop (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>C#{value}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
label</td>
    <td>label</td>
    <td>category (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>L#{value}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>


Notes:

* config_type: Entity type (sys)

* config_version: latest#sys#'date’ or history#recipe#’date’ 

    *  latest#* denotes the latest config value.

    *  history#* is the history of changes.

### GSI design

N/A

## b-c-product

This table contains all the customer/machine related configurations entities according to REF#1. The following entities from REF#1 are packed into this table:

* Customer

* Config Set

* Recipe

### Table design

<table>
  <tr>
    <td>Primary Key</td>
    <td></td>
    <td>

Attributes</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>item_key
 (PK) (S)</td>
    <td>sort_key 
(SK) (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>












customer#{customer_id}

</td>
    <td>customer_id</td>
    <td>customer_name (S)</td>
    <td>alias (S)</td>
    <td>address (S)</td>
    <td></td>
    <td>logo (S)</td>
    <td>creation_date (S)</td>
    <td>default_timezone (S)</td>
    <td>account_type (S)</td>
  </tr>
  <tr>
    <td></td>
    <td>C#{customer_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>farms</td>
    <td>name (S)</td>
    <td>timezone (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>F#{farm_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>localization set</td>
    <td>alias (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>L#{localization_set}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>machines</td>
    <td>serial_no (S)</td>
    <td>machine_type (S)</td>
    <td></td>
    <td></td>
    <td>pin (S)</td>
    <td>is_active (B)</td>
    <td>machine_status (S)</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>M#{machine_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>machine config</td>
    <td>config_name (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>M#{machine_id}#C#{config_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td> machine farms</td>
    <td>name (S)</td>
    <td>timezone (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>M#{machine_id}#F#{farm_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>




config-set#<config_id>


</td>
    <td>config_id</td>
    <td>config_name (S)</td>
    <td></td>
    <td>creation_date (S)</td>
    <td></td>
    <td>last_update (S)</td>
    <td></td>
    <td>aux_sensors (L)</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>CS#{config_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>recipe</td>
    <td>recipe_name (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>CR#{recipe_id}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>labels</td>
    <td>category (S)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>CL#{label}</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>


<table>
  <tr>
    <td>








recipe#{recipe_id}</td>
    <td>recipe_id</td>
    <td>recipe_name (S)</td>
    <td>creation_date (S)</td>
    <td>last_update (S)</td>
    <td>sampling_interval_secs (N)</td>
  </tr>
  <tr>
    <td></td>
    <td>





R#<config_id>

(this represents a single item)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>pulse_enable (b)</td>
    <td>pulse_flash_order (L)</td>
    <td>pulse_flash_duty_down (N)</td>
    <td>pulse_flash_duty_up (N)</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>pulse_intensity (M)</td>
    <td>pulse_integration_time (N)</td>
    <td>pulse_number_of_scans (N)</td>
    <td>solid_enable (B)</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>solid_intensity (M)</td>
    <td>solid_flash_order (L)</td>
    <td>solid_integration_time (N)</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>


### GSI design

**b-c-product-GSI1 - **This index is basically created to make extracting configuration by machine_id possible.

* Primary Key: 

    * PK: sort_key

    * SK: None

* Attributes: <ALL>

