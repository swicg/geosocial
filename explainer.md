# Geosocial on the social web

## Introduction

The Geosocial Task Force focuses on associating physical or logical location with social data, also known as [_geosocial_](https://en.wikipedia.org/wiki/Geosocial_networking) data.  For example, associating a specific city with a ActivityPub post, or announcing arrival at a specific event.

This Task Force is a part of the [W3C Social Web Incubator Community Group](https://github.com/swicg).

## Reports

 - [ActivityPub Personal Places](https://swicg.github.io/geosocial/personal-places.html) - This report describes an API for creating and maintaining a list of an actor's personal places. 

## Authors:

- Mike Waggoner ([@herebox@social.coop](https://social.coop/@herebox))
- Jeremiah Lee ([@Jeremiah@alpaca.gold](https://alpaca.gold/@Jeremiah))
- Evan Prodromou ([@evan@cosocial.ca](https://cosocial.ca/@evan))

## Participate

- [Issue tracker](https://github.com/swicg/geosocial)
- [Discussion forum](https://www.w3.org/community/SocialCG/)

## Table of Contents
<!-- Generate a Table of Contents for using [doctoc](https://github.com/thlorenz/doctoc) -->

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [User-Facing Problem](#user-facing-problem)
- [Core concepts](#core-concepts)
- [Proposed Approach - Place IDs](#proposed-approach---place-ids)
- [Proposed Approach - Geotagging](#proposed-approach---geotagging)
- [Proposed Approach - Checking in](#proposed-approach---checking-in)
- [Proposed Approach - Microsyntax](#proposed-approach---microsyntax)
- [Additional Use Cases](#additional-use-cases)
  - [Geotagging](#geotagging)
  - [Checking in](#checking-in)
  - [Consuming use cases](#consuming-use-cases)
- [Vocabulary Detail](#vocabulary-detail)
  - [Object](#object)
  - [Place](#place)
  - [Activity Types](#activity-types)
- [Trust and safety considerations](#trust-and-safety-considerations)
- [Alternatives considered](#alternatives-considered)
- [References & acknowledgements](#references--acknowledgements)
- [Draft notes](#draft-notes)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## User-Facing Problem

As a reader, I would like to filter content by location.

As an author, I would like to include location data in social web activities.

As an author, I would like to include location data in plaintext content.

## Core concepts 

[Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/) includes vocabulary for  <cite><a href="https://www.w3.org/TR/activitystreams-vocabulary/#places">places</a></cite> and <cite><a href="https://www.w3.org/TR/activitystreams-vocabulary/#motivations-geo">geo-social events</a></cite>.

For Example:

* AS2 Objects can include a _[location](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-location)_ attribute with a _[Place](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-place)_ value
* Activities like _[Arrive](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-arrive)_ are defined which allow a location attribute.

## Proposed Approach - Place IDs

See [ActivityPub Personal Places](https://swicg.github.io/geosocial/personal-places.html)

## Proposed Approach - Geotagging

Include a location attribute and Place value.

For example:

```
...
  "location": {
    "type": "Place",
    "name": "Los Angeles",
    "longitude": "-118.243680",
    "latitude": "34.052230",
  }
  ...
```

See a live example from Pixelfed at https://browser.pub/https://pixelfed.social/i/web/post/739027037396240803


## Proposed Approach - Checking in

Include [Arrive](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-arrive) activity

```
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "summary": "Sally arrived at work",
  "type": "Arrive",
  "actor": {
    "type": "Person",
    "name": "Sally"
  },
  "location": {
    "type": "Place",
    "name": "Work"
  },
  "origin": {
    "type": "Place",
    "name": "Home"
  }
}
```

## Proposed Approach - Microsyntax

( _As an ActivityPub user, I want to include microsyntax in my posts to identify locations, so that I can experiment with geosocial features without server or client support._ [#16](https://github.com/swicg/geosocial/issues/16) )

* [Microsyntax](https://swicg.github.io/geosocial/microsyntax.html)
* [Open Location Codes](https://en.wikipedia.org/wiki/Open_Location_Code) (OLC) also known as [Plus Codes](https://maps.google.com/pluscodes/)

## Additional Use Cases

 - See [Issues](https://github.com/swicg/geosocial/issues)

### Geotagging

These are use cases related to attaching location to another primary object.

- Where photo/video recorded https://github.com/swicg/geosocial/issues/4
- Photo/video about the location https://github.com/swicg/geosocial/issues/7
- Note/article where written https://github.com/swicg/geosocial/issues/5
- Note/article about the location https://github.com/swicg/geosocial/issues/6
- Microsyntax for location https://github.com/swicg/geosocial/issues/16

### Checking in

These are use cases related to announcing movement

- Current location https://github.com/swicg/geosocial/issues/13
- Check in https://github.com/swicg/geosocial/issues/1
- Check out https://github.com/swicg/geosocial/issues/2
- In transit https://github.com/swicg/geosocial/issues/3
- Plan to visit https://github.com/swicg/geosocial/issues/12
- Marking self as safe https://github.com/swicg/geosocial/issues/15


### Consuming use cases

- Cluster content by place https://github.com/swicg/geosocial/issues/10
- See related content by place https://github.com/swicg/geosocial/issues/9
- Comparing Places https://github.com/swicg/geosocial/issues/8


## Vocabulary Detail

### Object

The Object core type allows a [location](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-location) attribute.

### Place

A Place can be the value of a location attribute, and allow these additional attributes,

* accuracy
* altitude
* latitude
* longitude
* radius
* units

Place objects also inherit all attributes from the core object, including

* name
* duration

### Activity Types

Activity types include these geo-social events,

* [Arrive](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-arrive)
* Leave
* Travel

Activity objects also inherit all attributes from the core object, including

* location

## Trust and safety considerations

- "Avoid stalkers" https://github.com/swicg/geosocial/issues/11

## Alternatives considered

* Hashtags

## References & acknowledgements

Many thanks for valuable feedback and advice from:

- W3C Social Working Group community members

Thanks to the following proposals, projects, libraries, frameworks, and languages for their work on similar problems that influenced this proposal.

- [W3C Social Working Group](https://www.w3.org/wiki/Socialwg)
- [W3C Geolocation](https://www.w3.org/TR/geolocation/)

## Draft notes

The Geosocial Task Force exists to explore 

- [W3C explainer template](https://github.com/w3ctag/explainer-explainer/blob/main/template.md)
- [W3C Manual of Style](https://w3c.github.io/manual-of-style/)
-- [WAI style guide](https://www.w3.org/WAI/EO/wiki/Style)

Due to a wide variety of use cases, this explainer limits scope to summarize existing capabilities, catalog use cases, and highlight opportunities for further investigation.

Recommendations focus on [Activity Streams](https://www.w3.org/TR/activitystreams-core/) and [ActivityPub](https://www.w3.org/TR/activitypub/), and follows [W3C TAG writing effective explainers](https://tag.w3.org/explainers/).
