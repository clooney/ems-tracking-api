EMS Tracking API - PHP
================================
Use PHP to track EMS shipments with EMS Tracking API.

Features
--------
- Real-time EMS tracking.
- Batch EMS tracking.
- Other features to manage your EMS tracking.

Installation
------------

Installation is easy:

    $ composer require trackingmore/trackingmore-sdk-php

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your EMS shipments.

Usage
----------

Create a tracking (Real-time tracking):

      require('vendor/autoload.php');

      use Trackingmore\TrackingMoreException;
      use TrackingMore\Trackings;
        
      $key = 'your api key';
      $response = null;
      $trackings = new Trackings($key);
      
      try {
        $params = ['tracking_number'=>'EB809059138CN','courier_code'=>'ems-post'];
        $response = $trackings->createTracking($params);
      } catch (TrackingMoreException $e) {
        echo $e->getMessage();
      }

      print_r($response);

Create trackings (Max. 40 tracking numbers create in one call):

        require('vendor/autoload.php');

        use Trackingmore\TrackingMoreException;
        use TrackingMore\Trackings;
        
        $key = 'your api key';
        $response = null;
        $trackings = new Trackings($key);
        
        try {
            $params = [
                ['tracking_number'=>'EV046445981CN','courier_code'=>'ems-post'],
                ['tracking_number'=>'ED013441749CV','courier_code'=>'ems-post']
            ];
            $response = $trackings->batchCreateTrackings($params);
        } catch (TrackingMoreException $e) {
            echo $e->getMessage();
        }
        
        print_r($response);


Get status of the shipment:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['courier_code'=>'ems-post','created_date_min'=>'2023-08-23T06:00:00+00:00','created_date_max'=>'2023-09-05T07:20:42+00:00'];
        $response = $trackings->getTrackingResults($params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);


Update a tracking by ID:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['customer_name'=>'New name','note'=>'New tests order note'];
        $idString = '9dc05c81388cfb2e64fbc6ed4f14c1dc';
        $response = $trackings->updateTrackingByID($idString,$params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);
