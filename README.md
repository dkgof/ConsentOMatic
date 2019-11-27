# Consent-O-Matic

* [Introduction](#introduction)
* [Basic Structure](#basic-structure)
* [Detectors](#detectors)
* [Methods](#methods)
* [Actions](#actions)
    * [Click](#click)
    * [List](#list)
    * [Consent](#consent)
    * [Slide](#slide)
    * [If Css](#if-css)
    * [Wait For Css](#wait-for-css)
    * [For Each](#for-each)
    * [Hide](#hide)
* [Matchers](#matchers)
    * [Css](#css)
    * [Checkbox](#checkbox)
* [Consent](#consent)

## Introduction

## Basic Structure

A rule list for Consent-O-Matic is a JSON structure that contains the rules for detecting a CMP (Consent Management Provider), and
dealing with the CMP popup if its detected.

It contains 2 parts, `detectors` and `methods`.

```json
{
   "detectors": [],
   "methods": []
}
```

## Detectors

Detectors are the part that detects if a certain rule set should be applied. Basically, if a detector triggers, the methods will be applied.

Detector structure:
```json
{
   "presentMatcher": {}
   "showingMatcher": {}
}
```

The present matcher is used to detect if the CMP is present on the page.

Some CMP's still insert into the DOM when revisiting a page you have already consented to earlier, and therefor we only want to handle the consent form if its actually showing on the page. This is what the showing matcher is used for.

Both the present and showing matcher are of type [`Matcher`](#matchers).

## Methods

There are 3 methods supported by Consent-O-Matic. `OPEN_OPTIONS`, `DO_CONSENT`, `SAVE_CONSENT`

All the methods are optional, and if present the methods will be run in the order given above, when a detector is triggered.

## Actions

### Click

### List

### Consent

### Slide

### If Css

### Wait For Css

### For Each

### Hide

## Matchers

### Css

### Checkbox

## Consent
