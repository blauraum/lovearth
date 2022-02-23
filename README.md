# lovearth
LovEarth map
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Points on a map</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <script src="https://api.tiles.mapbox.com/mapbox-gl-js/v2.6.1/mapbox-gl.js"></script>
    <link
      href="https://api.tiles.mapbox.com/mapbox-gl-js/v2.6.1/mapbox-gl.css"
      rel="stylesheet"
    />
    <style>
      body {
        margin: 0;
        padding: 0;
      }
      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }
      .container-lg {
        padding-left: none;
      }
    </style>
  </head>
  <body>
    <div id="map"></div>
    <script>
      // The value for 'accessToken' begins with 'pk...'
      mapboxgl.accessToken =
        "pk.eyJ1IjoibG92ZWFydGgiLCJhIjoiY2t3MnExN2c4MGZpajJubmhnY3JsZjB1MyJ9.98jdEHBhonsPh2IH-ehyMw";
      const map = new mapboxgl.Map({
        container: "map",
        // Replace YOUR_STYLE_URL with your style URL.
        style: "mapbox://styles/lovearth/ckwlpdozh43i215n0qogrjqpt",
        center: [135.015013, -30.048477],
        zoom: 2.5,
      });

      // Code from the next step will go here.
      /* 
Add an event listener that runs
  when a user clicks on the map element.
*/
      map.on("click", (event) => {
        // If the user clicked on one of your markers, get its information.
        const features = map.queryRenderedFeatures(event.point, {
          layers: ["le-stockists-minimised", "le-dropoff-points"], // replace with your layer name
        });
        if (!features.length) {
          return;
        }
        const feature = features[0];

        // Code from the next step will go here.
        /* 
    Create a popup, specify its options 
    and properties, and add it to the map.
  */
        const popup = new mapboxgl.Popup({ offset: [0, -15] })
          .setLngLat(feature.geometry.coordinates)
          .setHTML(
            `<h3>${feature.properties.name}</h3>
            <p>${feature.properties.street}</br>${feature.properties.suburb} ${feature.properties.state} ${feature.properties.postcode}</br><a href="${feature.properties.website}">${feature.properties.website}</a></br> email: ${feature.properties.email}</a></br>phone: ${feature.properties.phone}</p>`
          )
          .addTo(map);
      });
    </script>
  </body>
</html>
