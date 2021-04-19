# About NSO RESTCONF API

## How to use NSO RESTCONF API via CNC

Cisco Network Services Orchestrator (NSO) supported RESTCONF API can be accessed from the Crosswork Network Controller (CNC) API Gateway endpoint using the same authentication mechanism used to access other CNC APIs when NSO is added to the CNC as a NSO Provider.
For information on adding Cisco NSO Providers, please refer to document *Get Started With Crosswork Network Controller*

The following is the CNC API Gateway endpoint (base URL path) to access the NSO supported RESTCONF API.

><https://{{cnc.host}}:{{cnc.port}}/crosswork/proxy/nso/restconf/...?async-commit-queue=true>

_Note, the (POST, PUT, PATCH and DELETE) calls should be sent with an additional query parameter "?async-commit-queue=true" for setting commit-queue async._

## Examples

### Create SR-TE policy with curl

```sh
curl --request POST 'https://10.194.63.232:30603/crosswork/proxy/nso/restconf/data/cisco-sr-te-cfp:sr-te/cisco-sr-te-cfp-sr-policies:policies?async-commit-queue=true' \
--header 'Content-Type: application/yang-data+json' \
--header 'Accept: application/yang-data+json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImlzRnJvbU5ld0xvZ2luIjoidHJ1ZSIsInBvbGljeV9pZCI6ImFkbWluIiwiYXV0aGVudGljYXRpb25EYXRlIjoiMjAyMC0wNS0xMVQwODoyNDo1Ni43NThaW0dNVF0iLCJzdWNjZXNzZnVsQXV0aGVudGljYXRpb25IYW5kbGVycyI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJpc3MiOiJodHRwOlwvXC9sb2NhbGhvc3Q6NTQ4OVwvU1NPIiwibGFzdF9uYW1lIjoic21pdGgiLCJjcmVkZW50aWFsVHlwZSI6IlVzZXJuYW1lUGFzc3dvcmRDcmVkZW50aWFsIiwiYXVkIjoiaHR0cHM6XC9cLzEwLjE5NC42My4yMzI6MzA2MDNcL2FwcC1kYXNoYm9hcmQiLCJhdXRoZW50aWNhdGlvbk1ldGhvZCI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJsb25nVGVybUF1dGhlbnRpY2F0aW9uUmVxdWVzdFRva2VuVXNlZCI6ImZhbHNlIiwiY2hhbmdlX3B3ZCI6ImZhbHNlIiwiZXhwIjoxNTg5MjE0Mjk5LCJpYXQiOjE1ODkxODU0OTksImZpcnN0X25hbWUiOiJqb2huIiwianRpIjoiU1QtMTMteE9ISi1WM0JQRExWaHFfaGwtdUVZM2VJbk52NEc3S2wxX0xzX1ZQTFVjZ1YtRnVBUEFXS2ZhcjdjMkJDUXBuY2F1LUJPVk9hbk1TaWZEczdaZGRSemtFQ3UxQkx6aWVlRDVSNElJNVlyQmZjSkRXaW9lNlN3RVhVaEpuakdjQTI4RnpJYVIzcGNaM3E4b2diMHdxMkFPcU5Lc0ZtcUlWMS1jYXMtN2M2YmY0YzU4NC13cng5OSJ9.OPnqZZ2eKqyGjngUizmw_hBY1iQNUxsVyrfcK2GGyi8HWlLTSTzDzNMoX_QceLQ8B_0sF3Oo0VEc3dinOgRTSg' \
--data-raw '{
    "cisco-sr-te-cfp-sr-policies:policy": [
        {
            "name": "srte_c_7008_ep_154.154.72.36",
            "color": 7008,
            "head-end": [
                {
                    "name": "TSDN-PE-1"
                }
            ],
            "path": [
                {
                    "preference": 7,
                    "dynamic": {
                        "constraints": {
                            "affinity": {
                                "rule": [
                                    {
                                        "action": "include-any",
                                        "color": [
                                            "1"
                                        ]
                                    }
                                ]
                            }
                        }
                    }
                }
            ],
            "tail-end": "154.154.72.36"
        }
    ]
}'
```

### Update SR-TE policy with curl

```sh
curl --request PATCH 'https://10.194.63.232:30603/crosswork/proxy/nso/restconf/data/cisco-sr-te-cfp:sr-te/cisco-sr-te-cfp-sr-policies:policies/policy=api-test-sr-policy1' \
--header 'Content-Type: application/yang-data+json' \
--header 'Accept: application/yang-data+json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImlzRnJvbU5ld0xvZ2luIjoidHJ1ZSIsInBvbGljeV9pZCI6ImFkbWluIiwiYXV0aGVudGljYXRpb25EYXRlIjoiMjAyMC0wNS0xMVQwODoyNDo1Ni43NThaW0dNVF0iLCJzdWNjZXNzZnVsQXV0aGVudGljYXRpb25IYW5kbGVycyI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJpc3MiOiJodHRwOlwvXC9sb2NhbGhvc3Q6NTQ4OVwvU1NPIiwibGFzdF9uYW1lIjoic21pdGgiLCJjcmVkZW50aWFsVHlwZSI6IlVzZXJuYW1lUGFzc3dvcmRDcmVkZW50aWFsIiwiYXVkIjoiaHR0cHM6XC9cLzEwLjE5NC42My4yMzI6MzA2MDNcL2FwcC1kYXNoYm9hcmQiLCJhdXRoZW50aWNhdGlvbk1ldGhvZCI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJsb25nVGVybUF1dGhlbnRpY2F0aW9uUmVxdWVzdFRva2VuVXNlZCI6ImZhbHNlIiwiY2hhbmdlX3B3ZCI6ImZhbHNlIiwiZXhwIjoxNTg5MjE0Mjk5LCJpYXQiOjE1ODkxODU0OTksImZpcnN0X25hbWUiOiJqb2huIiwianRpIjoiU1QtMTMteE9ISi1WM0JQRExWaHFfaGwtdUVZM2VJbk52NEc3S2wxX0xzX1ZQTFVjZ1YtRnVBUEFXS2ZhcjdjMkJDUXBuY2F1LUJPVk9hbk1TaWZEczdaZGRSemtFQ3UxQkx6aWVlRDVSNElJNVlyQmZjSkRXaW9lNlN3RVhVaEpuakdjQTI4RnpJYVIzcGNaM3E4b2diMHdxMkFPcU5Lc0ZtcUlWMS1jYXMtN2M2YmY0YzU4NC13cng5OSJ9.OPnqZZ2eKqyGjngUizmw_hBY1iQNUxsVyrfcK2GGyi8HWlLTSTzDzNMoX_QceLQ8B_0sF3Oo0VEc3dinOgRTSg' \
--data-raw '{
    "cisco-sr-te-cfp-sr-policies:policy": [
        {
            "name": "api-test-sr-policy1",
            "color": 7007,
            "head-end": [
                {
                    "name": "PE-B"
                }
            ],
            "path": [
                {
                    "preference": 8,
                    "dynamic": {
                        "constraints": {
                            "affinity": {
                                "rule": [
                                    {
                                        "action": "include-any",
                                        "color": [
                                            "1"
                                        ]
                                    }
                                ]
                            }
                        }
                    }
                }
            ],
            "tail-end": "100.100.100.7"
        }
    ]
}'
```

### Delete SR-TE policy with curl

```sh
curl --request DELETE 'https://10.194.63.232:30603/crosswork/proxy/nso/restconf/data/cisco-sr-te-cfp:sr-te/cisco-sr-te-cfp-sr-policies:policies/policy=api-test-sr-policy1?async-commit-queue=true' \
--header 'Content-Type: application/yang-data+xml' \
--header 'Accept: application/yang-data+xml' \
--header 'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImlzRnJvbU5ld0xvZ2luIjoidHJ1ZSIsInBvbGljeV9pZCI6ImFkbWluIiwiYXV0aGVudGljYXRpb25EYXRlIjoiMjAyMC0wNS0xMVQwODoyNDo1Ni43NThaW0dNVF0iLCJzdWNjZXNzZnVsQXV0aGVudGljYXRpb25IYW5kbGVycyI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJpc3MiOiJodHRwOlwvXC9sb2NhbGhvc3Q6NTQ4OVwvU1NPIiwibGFzdF9uYW1lIjoic21pdGgiLCJjcmVkZW50aWFsVHlwZSI6IlVzZXJuYW1lUGFzc3dvcmRDcmVkZW50aWFsIiwiYXVkIjoiaHR0cHM6XC9cLzEwLjE5NC42My4yMzI6MzA2MDNcL2FwcC1kYXNoYm9hcmQiLCJhdXRoZW50aWNhdGlvbk1ldGhvZCI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJsb25nVGVybUF1dGhlbnRpY2F0aW9uUmVxdWVzdFRva2VuVXNlZCI6ImZhbHNlIiwiY2hhbmdlX3B3ZCI6ImZhbHNlIiwiZXhwIjoxNTg5MjE0Mjk5LCJpYXQiOjE1ODkxODU0OTksImZpcnN0X25hbWUiOiJqb2huIiwianRpIjoiU1QtMTMteE9ISi1WM0JQRExWaHFfaGwtdUVZM2VJbk52NEc3S2wxX0xzX1ZQTFVjZ1YtRnVBUEFXS2ZhcjdjMkJDUXBuY2F1LUJPVk9hbk1TaWZEczdaZGRSemtFQ3UxQkx6aWVlRDVSNElJNVlyQmZjSkRXaW9lNlN3RVhVaEpuakdjQTI4RnpJYVIzcGNaM3E4b2diMHdxMkFPcU5Lc0ZtcUlWMS1jYXMtN2M2YmY0YzU4NC13cng5OSJ9.OPnqZZ2eKqyGjngUizmw_hBY1iQNUxsVyrfcK2GGyi8HWlLTSTzDzNMoX_QceLQ8B_0sF3Oo0VEc3dinOgRTSg' \
--data-raw ''
```
## NSO RESTCONF Notifications/Streams via CNC

Cisco Network Services Orchestrator (NSO) supported RESTCONF Notifications/Streams which can be accessed from the Crosswork Network Controller (CNC) API Gateway.
The following is the CNC API Gateway endpoint (base URL path) to list Notificaiton Streams supported

>https://{{cnc.host}}:{{cnc.port}}/crosswork/proxy/nso/restconf/data/ietf-restconf-monitoring:restconf-state/streams

## Examples

### Subscribe to service-state-change notificatons stream 

```sh
curl -k -X GET -H 'Content-Type: application/json' 'https://${host}:${port}/crosswork/proxy/nso/restconf/streams/service-state-changes/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImlzRnJvbU5ld0xvZ2luIjoidHJ1ZSIsInBvbGljeV9pZCI6ImFkbWluIiwiYXV0aGVudGljYXRpb25EYXRlIjoiMjAyMC0wNS0xMVQwODoyNDo1Ni43NThaW0dNVF0iLCJzdWNjZXNzZnVsQXV0aGVudGljYXRpb25IYW5kbGVycyI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJpc3MiOiJodHRwOlwvXC9sb2NhbGhvc3Q6NTQ4OVwvU1NPIiwibGFzdF9uYW1lIjoic21pdGgiLCJjcmVkZW50aWFsVHlwZSI6IlVzZXJuYW1lUGFzc3dvcmRDcmVkZW50aWFsIiwiYXVkIjoiaHR0cHM6XC9cLzEwLjE5NC42My4yMzI6MzA2MDNcL2FwcC1kYXNoYm9hcmQiLCJhdXRoZW50aWNhdGlvbk1ldGhvZCI6IlF1ZXJ5RGF0YWJhc2VBdXRoZW50aWNhdGlvbkhhbmRsZXIiLCJsb25nVGVybUF1dGhlbnRpY2F0aW9uUmVxdWVzdFRva2VuVXNlZCI6ImZhbHNlIiwiY2hhbmdlX3B3ZCI6ImZhbHNlIiwiZXhwIjoxNTg5MjE0Mjk5LCJpYXQiOjE1ODkxODU0OTksImZpcnN0X25hbWUiOiJqb2huIiwianRpIjoiU1QtMTMteE9ISi1WM0JQRExWaHFfaGwtdUVZM2VJbk52NEc3S2wxX0xzX1ZQTFVjZ1YtRnVBUEFXS2ZhcjdjMkJDUXBuY2F1LUJPVk9hbk1TaWZEczdaZGRSemtFQ3UxQkx6aWVlRDVSNElJNVlyQmZjSkRXaW9lNlN3RVhVaEpuakdjQTI4RnpJYVIzcGNaM3E4b2diMHdxMkFPcU5Lc0ZtcUlWMS1jYXMtN2M2YmY0YzU4NC13cng5OSJ9.OPnqZZ2eKqyGjngUizmw_hBY1iQNUxsVyrfcK2GGyi8HWlLTSTzDzNMoX_QceLQ8B_0sF3Oo0VEc3dinOgRTSg' 
''
```

## More Details

To get more details about the NSO support on the RESTCONF API, please visit [Network Services Orchestrator Software - 5.4.2](https://software.cisco.com/download/home/286323467/type/286283941/release/5.4.2) page on the web.

- Download and untar NSO Documentation file **nso-5.4.2.doc.tar.gz**
- Use the documentation at **doc/html/nso_northbound/ncs.northbound.restconf.html**
