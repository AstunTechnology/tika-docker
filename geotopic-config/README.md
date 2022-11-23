# GeoTopicParser

## Set-up

Set up the lucene-geo-gazetteer as per https://cwiki.apache.org/confluence/display/TIKA/GeoTopicParser and set it running in server mode.

Edit https://github.com/AstunTechnology/tika-docker/blob/geotopicparser/geotopic-config/org/apache/tika/parser/geo/topic/GeoTopicConfig.properties to set the `gazetter.rest.api` to point at the URL for your lucene-geo-gazetteer. This should be the root url including the port (defaults to 8765). Note the spelling of `gazetter`!

Note also that if you are running lucene-geo-gazetteer natively, and this docker instance on the same host, then you need to set `gazetter.rest.api` to the `docker_gateway_host` URL, which is generally 172.17.0.1

Download https://opennlp.sourceforge.net/models-1.5/en-ner-location.bin and place it in `./org/apache/tika/parser/geo/topic`

## Usage

From the root directory `tika-docker` run `docker-compose -f docker-compose-tika-geo.yml up -d`

Using the sample polar.geot file, run the following to extract locations:

    curl -T polar.geot -H "Content-Disposition: attachment; filename=polar.geot" http://localhost:9998/rmeta

If it's correctly working it will return the following (formatted for readability):

    [{"Content-Type":"application/geotopic",
        "Geographic_LATITUDE":"35.0",
        "Geographic_LONGITUDE":"105.0",
        "Geographic_NAME":"People’s Republic of China",
        "Optional_LATITUDE1":"39.76",
        "Optional_LONGITUDE1":"-98.5",
        "Optional_NAME1":"United States",
        "X-Parsed-By":["org.apache.tika.parser.CompositeParser","org.apache.tika.parser.geo.topic.GeoParser"],
        "X-TIKA:embedded_depth":"0",
        "X-TIKA:parse_time_millis":"48",
        "resourceName":"polar.geot"}]

