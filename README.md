# Covid-19Paths

## Description

This is an app meant to try to notify people could have had interactions with those who have tested positive for Covid-19. 

The app will poll a person's location every x amount of minutes and push this data to the cloud.
If a person receives a positive test, the app will then find all of the other people who have been in the same places at approximately the same time, and notify them with a warning.

## Architecture

The location data will be stored as a geohash in an influxdb. The app will publish a user's location to a queue with a timestamp and a subscribed worker will insert that data into the database.
Upon someone telling the app they tested positive, all of the locations the person had been for the previous two weeks is pulled and people in the same approximate location at the same approximate time will recieve a push notification.

## How to determine who gets a push notification

We check if a person was at the same place as the person who tested positive within the hour.