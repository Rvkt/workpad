---
title: "Water Sports & Sailing Apps"
source: "https://stormglass.io/watersports/"
author:
  - "[[stormglass]]"
published: 2019-10-01
created: 2026-10-22
description: "Global Weather API providing high-resolution weather forecasts and historical data for Maritime, Green Energy and Agricultural applications."
tags:
  - "clippings"
---
#### Weather Forecasts in Watersport Apps

Using smarphone apps to be able to get insight on where and when to go fishing, sailing or surfing is becoming increasingly popular and it’s easy to understand why. It’s simply a great way to increase the performance of your surf or fishing session without having to spend a vast amount of time reaserching weather forecasts.

The Storm Glass API is the perfect data source to power your application with global high-resolution forecasts via one single integration. By sending in a coordinate and filter out the data that’s actually relevant for the app users, you will be able to create a quick and responsive experience for the users.

The most relevant weather parameters for watersports available in the API is:

- Wave – height, direction & period
- Swell – height, direction & period
- Secondary Swell – height, direction & period
- Wind Wave – height, direction & period
- Wind (multiple altitudes) – speed, direction & gust
- Tide, Water- & Air Temperature
- Sunrise / Sunset

For Fishing applications astronomy data is also highly relevant:

- Moonrise / Moonset
- Moon Phase
- Closest Moonphase & Moon Fraction

#### API Request Example

Below you’ll find an API request example showing how to access the weather parameters most relelevant to watersports apps.

###### Weather for single coordinate

```js
const lat = 45.7;

const lng = -6.0;

const params = [

  'secondarySwellDirection', 'secondarySwellHeight', 'secondarySwellPeriod',

  'windWaveDirection', 'windWaveHeight', 'windWavePeriod',

  'swellDirection', 'swellHeight', 'swellPeriod',

  'waveDirection', 'waveHeight', 'wavePeriod',

  'windDirection', 'windSpeed', 'gust',

  'waterTemperature',

].join(',');

fetch(\`https://api.stormglass.io/v2/weather/point?lat=${lat}&lng=${lng}&params=${params}\`, {

  headers: {

     // Get your key by signing up.

    'Authorization': '2c16411d-8f11-4565-98a8-321c4e3eef9c'

  }

}).then((response) => response.json()).then((jsonData) => {

  // Do something with response data.

});
```

[view raw](https://gist.github.com/caalle/08594c77ada8a2a40651438e794aa4fc/raw/fa6e4ccac446bde376c18c7d8437fd1a9efef2e9/fishing.js) [fishing.js](https://gist.github.com/caalle/08594c77ada8a2a40651438e794aa4fc#file-fishing-js) hosted with ❤ by [GitHub](https://github.com/)

###### Astronomy for single coordinate

```js
const lat = 45.7;

const lng = -6.0;

fetch(\`https://api.stormglass.io/v2/astronomy/point?lat=${lat}&lng=${lng}\`, {

  headers: {

     // Get your key by signing up.

    'Authorization': '2c16411d-8f11-4565-98a8-321c4e3eef9c'

  }

}).then((response) => response.json()).then((jsonData) => {

  // Do something with tide data.

});
```

[view raw](https://gist.github.com/caalle/6825e72e2d4a75d30ed7487fbcd3cd09/raw/3b9899a8af1c37c6ca4260edb83f114c0fbacb5a/astronomy.js) [astronomy.js](https://gist.github.com/caalle/6825e72e2d4a75d30ed7487fbcd3cd09#file-astronomy-js) hosted with ❤ by [GitHub](https://github.com/)

###### Tides for single coordinate

```js
const lat = 45.7;

const lng = -6.0;

fetch(\`https://api.stormglass.io/v2/tide/extremes/point?lat=${lat}&lng=${lng}\`, {

  headers: {

     // Get your key by signing up.

    'Authorization': '2c16411d-8f11-4565-98a8-321c4e3eef9c'

  }

}).then((response) => response.json()).then((jsonData) => {

  // Do something with tide data.

});
```

[view raw](https://gist.github.com/caalle/a921a3fb37d8c8e935775b37537956c1/raw/9c52c0aec0872b2921a16ba66c20ed578c8fc112/single-extrema.js) [single-extrema.js](https://gist.github.com/caalle/a921a3fb37d8c8e935775b37537956c1#file-single-extrema-js) hosted with ❤ by [GitHub](https://github.com/)

For more information on how to use the Storm Glass API please have a look at the full documentation.

[Full documentation](https://docs.stormglass.io/)[Previous](https://stormglass.io/shipping/)