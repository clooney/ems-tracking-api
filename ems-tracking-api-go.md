EMS Tracking API - Go
================================
Use Go to track EMS shipments with EMS Tracking API.

Features
--------
- Real-time EMS tracking.
- Batch EMS tracking.
- Other features to manage your EMS tracking.

Installation
------------

Installation is easy:

    $ go mod init github.com/my/repo
    $ go get github.com/trackingmore-api/trackingmore-sdk-go

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

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }
      
      params := trackingmore.CreateTrackingParams{
        TrackingNumber: "EB809059138CN",
        CourierCode:    "ems-post",
      }      

      result, err := cli.CreateTracking(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Create trackings (Max. 40 tracking numbers create in one call):

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }
      
      params := []trackingmore.CreateTrackingParams{
          {
          TrackingNumber: "EV046445981CN",
          CourierCode:    "ems-post",
          },
          {
          TrackingNumber: "ED013441749CV",
          CourierCode:    "ems-post",
          },
      }   

      result, err := cli.BatchCreateTrackings(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Get status of the shipment:

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }

      params := trackingmore.GetTrackingResultsParams{
        CreatedDateMin: "2023-08-23T06:00:00+00:00",
        CreatedDateMax: "2023-09-05T07:20:42+00:00",
      }  

      result, err := cli.GetTrackingResults(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Update a tracking by ID:

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }

      params := trackingmore.UpdateTrackingParams{
        CustomerName: "New name",
        Note:         "New tests order note",
      }
      idString := "9dc05c81388cfb2e64fbc6ed4f14c1dc"
      
      result, err := cli.UpdateTrackingByID(context.Background(), idString, params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }
