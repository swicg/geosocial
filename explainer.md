# Geosocial on the social web

## Draft notes

Goal is to explain what the Geosocial Task Force is interested in exploring.

- [W3C explainer template](https://github.com/w3ctag/explainer-explainer/blob/main/template.md)
- [W3C Manual of Style](https://w3c.github.io/manual-of-style/)
-- [WAI style guide](https://www.w3.org/WAI/EO/wiki/Style)

Due to a wide variety of use cases, this explainer limits scope to summarize existing capabilities, catalog use cases, and highlight opportunities for further investigation.

Recommendations focus on [Activity Streams](https://www.w3.org/TR/activitystreams-core/) and [ActivityPub](https://www.w3.org/TR/activitypub/), and follows [W3C TAG writing effective explainers](https://tag.w3.org/explainers/).

## Authors:

- Mike Waggoner ([@herebox@social.coop](https://social.coop/@herebox))
- Jeremiah Lee ([@Jeremiah@alpaca.gold](https://alpaca.gold/@Jeremiah))
- Author 3 ([Affiliation 2])
- etc.

## Participate

- [Issue tracker](https://github.com/swicg/geosocial)
- [Discussion forum](https://www.w3.org/community/SocialCG/)

## Table of Contents
<!-- Generate a Table of Contents for using [doctoc](https://github.com/thlorenz/doctoc) -->

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

  - [Introduction](#introduction)
  - [Core concepts](#core-concepts)
    - [Place vocabulary](#place-vocabulary)
    - [Activity vocabulary](#activity-vocabulary)
  - [Creation use cases](#creation-use-cases)
    - [Geotagging](#geotagging)
    - [Checking in](#checking-in)
  - [Consuming use cases](#consuming-use-cases)
  - [Trust and safety consideations](#trust-and-safety-consideations)
    - [TODO unplaced stories](#todo-unplaced-stories)
  - [References & acknowledgements](#references--acknowledgements)
- [Legacy draft notes](#legacy-draft-notes)
  - [Use Cases](#use-cases)
  - [History](#history)
  - [Types of Places](#types-of-places)
  - [Syntax](#syntax)
    - [ActivityPub](#activitypub)
    - [Plaintext](#plaintext)
    - [Unique IDs](#unique-ids)
  - [Challenges](#challenges)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction

Here we focus on including physical or logical location with social data, also known as _geosocial_ data.  For example, associating a specific city with a Mastodon post, or announcing arrival at a specific event.

## User-Facing Problem

As a reader, I would like to filter content by location.

As an author, I would like to include location data in social web activities.

As an author, I would like to include location data in plaintext content.

## Core concepts 

[Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/) includes vocabulary for  <cite><a href="https://www.w3.org/TR/activitystreams-vocabulary/#places">places</a></cite> and <cite><a href="https://www.w3.org/TR/activitystreams-vocabulary/#motivations-geo">geo-social events</a></cite>.

For Example:

* AS2 Objects can include a _[location](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-location)_ attribute with a _[Place](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-place)_ value
* Activities like _[Arrive](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-arrive)_ are defined which allow a location attribute.


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
    "country": "USA"
  }
  ...
```

See a live example from Pixelfed at https://browser.pub/https://pixelfed.social/i/web/post/739027037396240803

*Note that _country_ is not a defined attribute for location.

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

## Proposed Approach - Place IDs

Include a JSON-LD uri as an @id attribute, e.g. https://places.pub/way/132605490

```
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/note/123456",
  "type": "Note",
  "content": "<p>This place is great!</p>",
  "location": {
    "id": "https://places.pub/way/132605490",
    "type": "Place",
    "name": "DNA Lounge"
  }
}
```

* [OSM Element](https://wiki.openstreetmap.org/wiki/Elements) ID
  * As Activity Pub Objects via JSON-LD
    * Example with [places.pub](https://places.pub/)
  * OSM Element attributes
    * node
    * way
    * relation
* [Geohash](https://en.wikipedia.org/wiki/Geohash)
* Default units https://github.com/swicg/geosocial/issues/17

## Proposed Approach - Microsyntax

( _As an ActivityPub user, I want to include microsyntax in my posts to identify locations, so that I can experiment with geosocial features without server or client support._ [#16](https://github.com/swicg/geosocial/issues/16) )

* [Open Location Codes](https://en.wikipedia.org/wiki/Open_Location_Code) (OLC) also known as [Plus Codes](https://maps.google.com/pluscodes/)

## Creation use cases

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


## Consuming use cases

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

- [Person 1]
- [Person 2]
- [etc.]

Thanks to the following proposals, projects, libraries, frameworks, and languages
for their work on similar problems that influenced this proposal.

- [Framework 1]
- [Project 2]
- [Proposal 3]
- [etc.]


----

# Legacy draft notes

* en:wiki
	* https://en.wikipedia.org/wiki/Geosocial_networking
	* https://en.wikipedia.org/wiki/Collaborative_mapping
	* https://en.wikipedia.org/wiki/Location_inference
	* https://en.wikipedia.org/wiki/Location_awareness
	* https://en.wikipedia.org/wiki/Crowdmapping
* Research
	* https://www.oswego.edu/celt/geosocial-media-web-goes-hyperlocal
* Commercial
	* REGIS https://sitesusa.com/Data/Geosocial
	* spatial.ai https://www.spatial.ai/post/the-essential-guide-to-geosocial-data
	* https://digistream.com/solutions/geosocialseries
		* "understanding how a location has evolved over an extended period of time, as well as deconstructing highly complex incidents and large media events."
	* https://grabgeo.com/ - Geo-monitoring for Android, iOS


## Use Cases

* Place Information
	* News
	* Photos
	* Recommendations
	* Reviews
* Chat
	* Proximity
	* Location subject focus
* Check-ins - Lifelogging
	* Private / Individual?
	* Social
	* Pathing - Sets of venues in an order
* Trust and Safety
	* Shared location with trusted contacts
	* Identifying risk
		* e.g. high / low activity
	* Avoiding risk
	* Multi-factor authentication ( Location services on mobile device )
	* Self-organizing marginalized populations ( e.g. migrants )
* Discovery of places
	* ...
* Discovery of pathing / routing
	* Activity heatmaps (e.g. Strava)
	* Traffic
* Discovery of people
	* Public - Meeting new people / Dating / Group organization
	* Trusted - Friends who happen to be nearby
	* Private - Group organization
	* Observed - Social graph by proximity
	* Inference - Expected based on social graph
	* Future - Expected proximity in the future
	* Expertise - Location experts
* Discovery of events
	* ...
* Gaming
* Fictional places
* Mapping
	* Crowdmapping / citizen science
		* ebird
		* earthquakes
		* weather
		* air quality
		* mushroom hunting
* Data analysis / Aggregation
	* Recreating events based on geo-tagged social posts and images
	* Census data / Demographic analysis
	* Vehicle traffic data
		* Maps live vehicle traffic
		* Congestion pricing
		* Transit applications
	* Pedestrian traffic data
		* Civil planning
		* Commercial applications
	* Weather

## History

* https://en.wikipedia.org/wiki/Category:Geosocial_networking

...

* Analog (Phone books, guest books, ...)
* Open Directory Project
* Dodgeball
* Gowalla
* Foursquare
* 2009 - Twitter announces Geotagging
* 2010-2021 - [Nearby](https://en.wikipedia.org/wiki/Nearby) app
* 2017-Present - [places.pub](https://gitlab.com/evanp/places-pub) service
* 2019-Present - [Radiate](https://en.wikipedia.org/wiki/Radiate_(app)) app
* Swarm
* BeeBot

## Types of Places

* Point of interest ( e.g. Null Island, Tokyo Tower)
* Mailing address
* Latitude and longitude
* Geopolitical
	* City, County, Country
* Geographical
	* Rocky Mountains, Continent of Europe, Nile River
* Unspecified Named Regions
	* Neighborhoods, USA's "Southwest"
* Mobile
	* M/V Wenatchee (ferry)
	* Empire Builder (train)
* Inside Another Place
* Vertically Relative
	* Eiffel Tower Observation Deck
	* Subway stations
* Ephemeral places
    * "Anywhere but here"
    * ...
* Fictional Places
	* Springfield from the Simpsons
	* Fraggle Rock
* Extra-Terrestrial
	* Moon, Mars
* Geohash - Deliberately obfuscated location? ( airbnb, risk mitigation )

## Syntax
### ActivityPub
* jsonld like places.pub

### Plaintext
### Unique IDs

## Challenges
* Trust and Safety
* Standardization