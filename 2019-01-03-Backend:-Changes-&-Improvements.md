---
title: Backend: Changes & Improvements
layout: post
author: farzadkhandan
permalink: /backend:-changes-&-improvements/
source-id: 1Oa-QO6vm4sULGh2AWfnKZpO2G_4Hhs7tnInKQsxAVsM
published: true
---
## Backend: Changes & Improvements

3 Jan, 2019

* Centralized Configuration Management

    * System configuration

        * Configurable Entities with UI

            * Customer

                * Farm

                * Bay

                * Phase

                * Rows

                * Machines

                * Machine Data

                    * Waves

                    * Videos

                    * Aux

                    * Labels

                    * Images

                    * Logs

            * Machine-config 

                * Multiple Configurations

                * Wave Recipes

                * Labels

        * Automated Customer/Farm Configuration using data from the Excel file 

        * Creating unified configuration API/lib/Service to be shared and used by all teams

        * Creating Admin Pages & Admin Website

        * ATTN: No Hard Coded Config/Entities/Enums at all

    * Infrastructure Configuration

        * Separate DevOps for Prod/Stage/Dev

        * Organized and unified configuration parameters with API/Service

* Moving toward a modern Data Lake

    * Design

    * Implement/Integrate

    * Test

    * Put into Production

* Introducing Analytics

    * Basic Reports

    * Live Dashboards

        * KPIs

    * Advanced Analytics

        * Predictive Maintenance

* Better Log Management 

    * Unified CloudWatch logging scheme

    * Log analytics (AWS Log Insights/3rd Parties)

