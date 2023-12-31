### This library is a modified version of arduino-esp32 HTTPClient.

The problem with the built-in library is that it only supports WiFiClient(Secure).

This modification supports the usage of any Client (EthernetClient, SSLClient, WifiClient, WiFiClientSecure, etc.).

To make this work, the following methods have been removed:

```C
    bool begin(String url);
    bool begin(String url, const char* CAcert);
    bool begin(String host, uint16_t port, String uri = "/");
    bool begin(String host, uint16_t port, String uri, const char* CAcert);
    bool begin(String host, uint16_t port, String uri, const char* CAcert, const char* cli_cert, const char* cli_key);
    void setConnectTimeout(int32_t connectTimeout);
```

An HTTPClientGeneric instance can be initialized by providing a client reference, so ensure that your client's
lifetime exceeds that of the HTTPClientGeneric instance.

```C
    bool begin(Client &client, String url);
    bool begin(Client &client, String host, uint16_t port, String uri = "/", bool https = false);
    bool begin(Client &client, IPAddress ip, uint16_t port, String uri = "/", bool https = false);
```
Added the IPAddress type for testing with local dev servers.

If connect timeout is an issue, consider overriding the default connection timeout macro 
if available in the client implementation library.

All other methods work exactly the same as the original HTTPClient.
