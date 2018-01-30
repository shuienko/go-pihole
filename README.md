# go-pihole
Go client for Pi-Hole API v3.0+

## Documentation
Available here: [![GoDoc](https://godoc.org/github.com/shuienko/go-pihole?status.svg)](https://godoc.org/github.com/shuienko/go-pihole)

## Example
```go
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/shuienko/go-pihole"
)

func main() {
	// Get environment variables
	piholeHost, ok := os.LookupEnv("PIHOLE_HOST")
	if !ok {
		log.Fatal("PIHOLE_HOST environment variable in NOT set")
	}

	apiToken, ok := os.LookupEnv("PIHOLE_TOKEN")
	if !ok {
		log.Fatal("PIHOLE_TOKEN environment variable is NOT set")
	}
    
    // Create connector object
	ph := gohole.PiHConnector{
		Host:  piholeHost,
		Token: apiToken,
	}

    // Get Pi-Hole Summary
    summary := ph.SummaryRaw()
    
    // Print AdsBlocked (last 24h)
    fmt.Println(summary.AdsBlocked)

    // Print statistics
    summary.Show()

    // Enable Pi-Hole
    err := ph.Enable()
    if err != nil {
        panic("Error")
    }

}
```