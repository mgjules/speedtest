# speedtest
[![CircleCI](https://circleci.com/gh/mgjules/speedtest.svg?style=shield)](https://circleci.com/gh/mgjules/speedtest) [![Maintainability](https://api.codeclimate.com/v1/badges/2130b46a52f698b3eaf1/maintainability)](https://codeclimate.com/github/mgjules/speedtest/maintainability) [![Test Coverage](https://api.codeclimate.com/v1/badges/2130b46a52f698b3eaf1/test_coverage)](https://codeclimate.com/github/mgjules/speedtest/test_coverage)

A golang package for running speedtests against speedtest.net.

## Usage
```go
package main

import (
	"fmt"

	"github.com/mgjules/speedtest"
)

func main() {
	client, err := speedtest.NewDefaultClient()
	if err != nil {
		fmt.Printf("error creating client: %v", err)
	}
	
	// Pass an empty string to select the fastest server
	server, err := client.GetServer("")
	if err != nil {
		fmt.Printf("error getting server: %v", err)
	}

	dmbps, err := client.Download(server)
	if err != nil {
		fmt.Printf("error getting download: %v", err)
	}

	umbps, err := client.Upload(server)
	if err != nil {
		fmt.Printf("error getting upload: %v", err)
	}

	fmt.Printf("Ping: %3.2f ms | Download: %3.2f Mbps | Upload: %3.2f Mbps\n", server.Latency, dmbps, umbps)
}

```
## Tests
`go test ./...`
## Thanks

Major thanks to @zpeters for the excellent [github.com/zpeters/speedtest](https://github.com/zpeters/speedtest) package, which server as a major starting off point for this repo.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/mgjules/speedtest. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The package is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
