# Generate the mocks for go interfaces
**First install the mockery:**
```
go install github.com/vektra/mockery/v2@v2.24.0terface
```
**Generate the mock:**
```
aafak@360726 MINGW64 ~/github-repos/Private-Cloud/app1 (main)
$ mockery --dir=internal/services --name=ClusterInterface  --filename=mock_ClusterInterface.go --output=./internal/mocks/services --outpkg=services --structname=MockClusterInterface
24 Jul 24 13:41 IST DBG failed to read in config error="Config File \".mockery\" Not Found in \"[C:\\\github-repos\\\\Private-Cloud\\\\hci-setup C:\\\\Users\\\\aafak\\github-repos\\\\Private-Cloud C:\\\\Users\\\\aafak\\github-repos C:\\\\Users\\\\aafakm C:\\\\Users\\\\aafakmoh C:\\\\Users C:\\\\]\"" version=v2.24.0
24 Jul 24 13:41 IST INF couldn't read any config file version=v2.24.0
24 Jul 24 13:41 IST INF Starting mockery dry-run=false version=v2.24.0
24 Jul 24 13:41 IST INF Using config:  dry-run=false version=v2.24.0
24 Jul 24 13:41 IST INF DISCUSSION: dynamic walking of project is being considered for removal in v3. Please provide your feedback at the linked discussion. discussion=https://github.com/vektra/mockery/discussions/549 dry-run=false pr=https://github.com/vektra/mockery/pull/548 version=v2.24.0
24 Jul 24 13:41 IST INF Walking dry-run=false version=v2.24.0
24 Jul 24 13:41 IST INF Generating mock dry-run=false interface=ClusterInterface qualified-name=github.com/aafak/app1/internal/services version=v2.24.0
24 Jul 24 13:41 IST INF writing mock to file dry-run=false interface=ClusterInterface qualified-name=github.com/aafak/app1/internal/services version=v2.24.0

aafak@360726 MINGW64 ~/github-repos/Private-Cloud/app1 (main)
```

```
--dir=internal/services    # Interface location
--name=ClusterInterface    # Name of the interface
--filename=mock_ClusterInterface.go   # Name of the mock file
--output=./internal/mocks/services    # Mock dir location
--outpkg=services   # Package name of the mock
--structname=MockClusterInterface   # Name of the mock structure

```
