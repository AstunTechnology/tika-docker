# GeoTopicParser

## Set-up

Set up the lucene-geo-gazetteer as per https://cwiki.apache.org/confluence/display/TIKA/GeoTopicParser and set it running in server mode.

Edit GeoTopicConfig.properties to set the `gazetter.rest.api`. Note the spelling!

Download https://opennlp.sourceforge.net/models-1.5/en-ner-location.bin and place it in `./org/apache/tika/parser/geo/topic`

## Usage

From the root directory `tika-docker` run `docker-compose -f docker-compose-tika-geo.yml up -d`

Using the sample polar.geot file, run the following to extract locations:

    curl -T polar.geot -H "Content-Disposition: attachment; filename=polar.geot" http://localhost:9998/rmeta

