# Consent-O-Matic

* [Introduction](#introduction)
* [Basic Structure](#basic-structure)
* [Detectors](#detectors)
* [Methods](#methods)
* [DOM Selection](#dom-selection)
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
   "presentMatcher": {},
   "showingMatcher": {}
}
```

The present matcher is used to detect if the CMP is present on the page.

Some CMP's still insert into the DOM when revisiting a page you have already consented to earlier, and therefor we only want to handle the consent form if its actually showing on the page. This is what the showing matcher is used for.

Both the present and showing matcher are of type [`Matcher`](#matchers).

## Methods

There are 3 methods supported by Consent-O-Matic. `OPEN_OPTIONS`, `DO_CONSENT`, `SAVE_CONSENT`

All the methods are optional, and if present the methods will be run in the order given above, when a detector is triggered.

Methods take on the form:
```json
{
   "name": "",
   "action": {}
}
```

Where the name is one of the 3 supported methods, and action is the action to execute.

## DOM Selection

Most actions and matchers have some target that they apply to. For this reason Consent-O-Matic has a DOM selection mechanism that can easily help with selecting the correct dom element.

```json
"parent": {
   "selector": ".some.css.selector",
   "textFilter": "someTextFilter",
   "styleFilter": {
      "option": "someStyleOption",
      "value": "someStyleValue",
      "negated": false
   },
   "displayFilter": true,
   "iframeFilter": false,
   "childFilter": {}
},
"target": {
   "selector": ".some.css.selector",
   "textFilter": "someTextFilter",
   "styleFilter": {
      "option": "someStyleOption",
      "value": "someStyleValue",
      "negated": false
   },
   "displayFilter": true,
   "iframeFilter": false,
   "childFilter": {}
}
```

There are 2 parts, `parent` and `target`. The `parent` is optional, if it exists it will be resolved first, and used as the starting point for `target`.

All the parameters to `parent` and `target` except `selector` are optional.

The selection method works by using the css selector from `selector` and then filtering the resulting DOM nodes via the various filters:

`textFilter` filters all nodes that does not include the given text. It can also be given as an array `"textFilter":["filter1", "filter2"]` and then it filters all nodes that does not include one of the given text filters.

`styleFilter` filters based on computedStyles. `option` is the style option to compare for example `position`, `value` is the value to compare against and `negated` sets if the option value should match or not match the given value.

`displayFilter` can be used to filter nodes based on if they are display hidden or not.

`iframeFilter` filters nodes based on if they are inside an iframe or not.

`childFilter` uses the same format as `parent` or `target` and is used to check that a specific child node exists, if not the current node is filtered.

Lets make an example dom selection:
```json
"parent": {
   "selector": ".myParent",
   "iframeFilter": true,
   "childFilter": {
      "selector": ".myChild",
      "textFilter": "Gregor"
   }
},
"target": {
   "selector": ".myTarget"
}
```
This selector first tries to find the `parent` chich is a DOM element with the class `myParent` that is inside an iframe and has a child DOM element with the class `myChild` that contains the text "Gregor".

Then using this parent as "root" it tries to find a DOM element with the class `myTarget`.

This could then be the target of an action or matcher.

## Actions

Actions are the part of Consent-O-Matic that actually do stuff. Some actions do something to a target selection, others have to do with control flow.

### Click

This action simulates a mouse click on its target.

Example:
```json
{
   "type": "click",
   "target": {
      "selector": ".myButton",
      "textFilter": "Save settings"
   }
}
```

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
