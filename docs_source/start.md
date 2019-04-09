# Welcome to Wirecard ePOS API Integration Guide

Purpose of this integration guide is to provide step by step instructions on how to integrate to Wirecard ePOS solution via REST API.

!!! Note
    Payment acceptance functionality is usually a subset of a larger solution so throughout this guide we refer to the functionality that you create with the Wirecard ePOS API as the payment acceptance, even though it may not be a standalone system.

### Who is this for?
For organizations (we call them partners) who want to utilize Wirecard ePOS API in order to enhance their solution with payment acceptance functionality. Merchants are the actual end-users of the payment acceptance functionality.

!!! Tip
    If you are new to the payment industry there are a lot of terms
    to learn. So, the terms partner, merchant, user, payment acceptance application
    and many others are all defined in [Glossary](glossary.md) to help you with this
    task. [Glossary](glossary.md) has also definitions for the most common acronyms you
    find in this integration guide, such as Purchase, Return, Payment transaction and others.

### How much is covered?
Our goal is to provide as much information as needed to successfully create a payment acceptance solution in the shortest possible time. [Core Integration](.) covers core functionality which has to be integrated. [Advanced Integration](.) covers value added functionality which is not mandatory.
 
### How technical is it?
 Partner team typically consists of a non-technical or semi-technical project manager and one or more developers who are technical. This guide is for the whole team so the information here ranges from non-technical to technical.
 
### What do I need to know?
Following skills are required:

- understanding of REST API calls
- understanding of JSON objects