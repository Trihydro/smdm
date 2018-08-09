# Service Monitor Device Management

## Description

This application is used internally to monitor the network status of Road Side Units (RSUs). This app monitors IPv4, IPv6 and DSRC network statuses and provides information visually on a map as well as charts and graphs in a dashboard format. It also provides information for active Traveler Information Messages (TIMs) and vehicle counts past an RSU.

## Release Notes

### Version 2.0
- First upload to GitHub

## Getting Started

### Prerequisites
ESRI's Web AppBuilder for ArcGIS (Developer Edition) version 2.8
- https://developers.arcgis.com/web-appbuilder/

ArcGIS Server - map services

ArcGIS Portal - web map

### Instructions

The following instructions describe the process to download, configure and create the web app.

#### Create map services
Required map services for the app to work properly:
- RSU Network
  - See SMDM_RSU.png diagram and notes below.
- RSU DSRC
  - See SMDM_RSU.png diagram and notes below.
- Active TIMs
  - See SMDM_ACTIVE_TIM.png diagram.

The RSU Network and RSU DSRC layers use the same data source and the values outlined below are expected in order for the app to work properly. 
- STATUS
  - RSU site status.
  - Expected values:
    - Existing
    - Proposed
    - Not in Service
- IPV4_STATUS_UP
  - IPv4 network status
  - Expected values:
    - 1
      - status up
    - 0
      - status other than up
- IPV6_STATUS_UP
  - IPv6 network status
  - Expected values:
    - 1
      - status up
    - 0
      - status other than up
- DSRC_STATUS_UP
  - DSRC status
  - Expected values:
    - 1
      - status up
    - 0
      - status other than up
- NETWORK_STATUS
  - IPv4 network status. This column is used to symbolize the RSU Network layer.
  - Expected values
    - green
      - IPv6 and IPv4 statuses are up.
    - yellow
      - IPv6 status is up IPv4 status is down.
    - orange
      - IPv6 status is down IPv4 status is up.
    - red
      - IPv6 and IPv4 statuses are down.
    - gray
      - IPv6 or IPv4 statuses are other.
    - not in service
      - RSU not in service.
    - proposed
      - RSU is proposed.
- DSRC_NETWORK_STATUS
  - DSRC network status. This column is used to symbolize the RSU DSRC layer.
  - Expected values:
    - green
      - DSRC status is up.
    - red
      - DSRC status is down.
    - gray
      - DSRC status is other.
    - not in service
      - RSU is not in service.
    - proposed
      - RSU is proposed.
      
The Active TIMs layers is joined to the RSU Network layer in the map service using the deviceid column.

Optional map services:
- Construction
- VSL
- Incidents
- Road Conditions

These map services are optional and if not used will need to be removed from the config.json and configs/AttributeTable/config_widgets_AttributeTable_Widget_30.json files.

#### Create web map
A web map is required for the Web AppBuilder template to work. One will need to be created and accessible on ArcGIS Portal.

#### Download and configure the config.json file
**Step 1**: Download the config.json file.

**Step 2**: Open the file for editing and modify the following lines of code to use your ArcGIS Portal/Server URLs:
  - Line 19: ArcGIS Portal URL
  - Line 398: ArcGIS Portal URL
  - Line 767: RSU Network layer URL
  - Line 1036: RSU Network layer URL
  - Line 1305: Active TIMs layer URL
 
 **Step 3**: Save edits.

#### Download and configure the configs folder
**Step 1**: Download the configs folder.

**Step 2**: Open the configs/AttributeTable/config_widgets_AttributeTable_Widget_30.json file for editing and modify the following lines of code to use your ArcGIS Server URLs. This is the only file in the configs directory that needs to be modified.
  - Line 7: RSU Network layer URL
  - Line 206: RSU DSRC layer URL
  - Line 405: Construction layer URL
  - Line 484: Variable Speed Limit (VSL) layer URL
  - Line 535: Incidents layer URL
  - Line 596: Road Conditions layer URL
  - Line 657: Active TIMs layer URL
 
 **Step 3**: Save edits.

#### Create, download and configure a new web app from Web AppBuilder for ArcGIS
**Step 1**: Open Web AppBuilder for ArcGIS and connect to the portal you are using for the web map.

**Step 2**: Create a new Infographic dashboard.

**Step 3**: Download the web app.

**Step 4**: In the root menu replace the config.json with the one you downloaded and configured above.

**Step 5**: In the root menu replace the configs folder with the one you downloaded and configured above.
