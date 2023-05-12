+++
fragment = "content"
weight = 10
background = "light"
title = "About Geostyler"
+++

Geostyler is about styling maps. Maybe you are a developer looking for a set of UI components 
to build custom and flexible styling widgets for your geospatial application. Maybe you 
are a cartographer trying to get the style you worked so hard on in your favorite (Q)GIS into the 
web. Or maybe you are a project lead worrying about migrating all your styles to that new fancy 
rendering engine everyone (and particular your boss) is talking about. The Geostyler ecosystem is 
here to help. 

###  React Library

One key project of the ecosystem is the React Library providing developers with widgets and 
tools to build powerfull and flexible UIs to style geodata over the web. To get an idea of 
it's features and capabilities you can have a look at the [Demo Application](https://geostyler.github.io/geostyler-demo/) or dive into the [Source Code](https://github.com/geostyler/geostyler-demo). If you want to to learn how to build your own custom map styling applications 
be sure to look into the [tutorials](/#tutorials) and the [documentation](https://geostyler.github.io/geostyler/latest/index.html).

### Style Parsers and Transformations

Geostyler supports multiple style formats used in the open source geospatial ecosystem: 
QML from QGIS, Mapbox JSON used in MapLibre, OpenLayers Styling Format and the OGC-standardized 
SLD format used by Geoserver. Each of those can be transformed into one another using 
internally the Geostyler style format. Each style parser is provided as seperate Github 
repository and NPM package. You can get an overview of the available style parsers and 
links [here](/parsers). Be aware that not every styling capability of a particular style 
is supported. Lucky for you, Geostyler is open source and it is easy to contribute and get 
involved in the community. Styles can either be transformed using javascript in your application 
or with the Geostyler client (CLI). 

### Batch Conversion with the Geostyler CLI 

The Geostyler client let's you convert single style files or entire directories from one of the 
supported styles into another. Assuming you have node installed on your system, installation 
is as easy as typing `npm install -g geostyler-cli`. Once you have the client installed you 
can transform a style from QGIS QML format to SLD directly from the command line: 

```
geostyler -s qgis -t sld -o output.sld input.qml
```

Be sure to have a look at the [repository](https://github.com/geostyler/geostyler-cli) for 
further instructions and examples. 

### Conversion over the Web

Maybe for your setup and workflow a conversion over the web via HTTP requests 
is the way to go. If so, be sure to have a look at the Geostyler API. Using GET and POST 
requests you can transform your style over the web. The REST API is built on top of the popular 
nodeJS framework express. Check out the [documentation](https://services.meggsimum.de/geostyler-rest/api-docs) and the [repository](https://github.com/geostyler/geostyler-rest). 
Similar to the example above the following curl call will transform a simple Mapbox (JSON-Format) style to SLD (XML): 


<!-- Erst Rücksprache mit Christian Mayer ob Meggsimum API verlinkt werden kann / soll -->
<!-- Alternative: Local dev-host dann müsste oben noch ein Satz rein, der darauf 
hinweist, dass eine API auf localhost gestartet werden muss -->
```sh
curl -X 'POST' \
  'https://services.meggsimum.de/geostyler-rest/api/rpc/transform?sourceFormat=Mapbox&targetFormat=SLD' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "version": 8,
  "name": "Demo Style",
  "layers": [
    {
      "id": "Rule 1",
      "type": "circle",
      "paint": {
        "circle-radius": 16,
        "circle-color": "#4b33c8"
      }
    }
  ]
}'
```

You will receive the following XML output as response: 

```xml 
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
  <StyledLayerDescriptor version="1.0.0" xsi:schemaLocation="http://www.opengis.net/sld StyledLayerDescriptor.xsd" xmlns="http://www.opengis.net/sld" xmlns:ogc="http://www.opengis.net/ogc" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <NamedLayer>
      <Name>Demo Style</Name>
      <UserStyle>
        <Name>Demo Style</Name>
        <Title>Demo Style</Title>
        <FeatureTypeStyle>
          <Rule>
            <Name>Rule 1</Name>
            <PointSymbolizer>
              <Graphic>
                <Mark>
                  <WellKnownName>circle</WellKnownName>
                  <Fill>
                    <CssParameter name="fill">#4b33c8</CssParameter>
                  </Fill>
                </Mark>
                <Size>32</Size>
              </Graphic>
            </PointSymbolizer>
          </Rule>
        </FeatureTypeStyle>
      </UserStyle>
    </NamedLayer>
  </StyledLayerDescriptor>
```
 
### Invitation 

We hope that Geostyler can help you building open geospatial tools 
and maps. If it does we invite you to get involved: Whether you 
are a developer providing bug fixes and features or a user improving 
the documentation or writing tutorials. We wish you happy and stylisch 
mapping.   



