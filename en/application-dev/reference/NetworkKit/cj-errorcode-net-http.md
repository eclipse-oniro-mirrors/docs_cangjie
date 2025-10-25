# HTTP Error Codes

> **Note:**
>
> This document only covers module-specific error codes. For universal error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 2300001 Unsupported Protocol

**Error Message**

Unsupported protocol.

**Error Description**

The protocol version is not supported by the server.

**Possible Causes**

The protocol version passed in is not supported by the server.

**Resolution Steps**

Verify the protocol version passed in and check the server implementation.

## 2300003 Malformed URL

**Error Message**

URL using bad/illegal format or missing URL.

**Error Description**

Malformed URL.

**Possible Causes**

The URL format passed in may be incorrect.

**Resolution Steps**

Check the URL format passed in.

## 2300005 Proxy Server DNS Resolution Failed

**Error Message**

Couldn't resolve proxy name.

**Error Description**

The proxy server's domain name cannot be resolved.

**Possible Causes**

The server URL is incorrect.

**Resolution Steps**

Verify the proxy server's URL.

## 2300006 Hostname Resolution Failed

**Error Message**

Couldn't resolve host name.

**Error Description**

The server's domain name cannot be resolved.

**Possible Causes**

1. The server URL passed in is incorrect.
2. Network connectivity issues.

**Resolution Steps**

1. Verify the server URL passed in.
2. Check the network connection.

## 2300007 Connection to Server Failed

**Error Message**

Couldn't connect to server.

**Error Description**

Failed to connect to the server.

**Possible Causes**

The URL format passed in is incorrect.

**Resolution Steps**

Check the URL format passed in.

## 2300008 Illegal Server Response

**Error Message**

Weird server reply.

**Error Description**

The server returned illegal data.

**Possible Causes**

The server returned non-HTTP formatted data due to an error.

**Resolution Steps**

Investigate the server implementation.

## 2300009 Remote Resource Access Denied

**Error Message**

Access denied to remote resource.

**Error Description**

Access to the remote resource is denied.

**Possible Causes**

The specified content is denied by the server.

**Resolution Steps**

Check the request content.

## 2300016 HTTP2 Framing Layer Error

**Error Message**

Error in the HTTP2 framing layer.

**Error Description**

HTTP2 layer error.

**Possible Causes**

The server does not support HTTP2.

**Resolution Steps**

Capture packets and verify if the server supports HTTP2.

## 2300018 Incomplete Server Response

**Error Message**

Transferred a partial file.

**Error Description**

The server returned incomplete data.

**Possible Causes**

May be related to the server implementation.

**Resolution Steps**

Investigate the server implementation.

## 2300023 Failed to Write Received Data to Disk/Application

**Error Message**

Failed writing received data to disk/application.

**Error Description**

Failed to write received data to disk/application.

**Possible Causes**

The application lacks file write permissions or the file to be downloaded exceeds 5MB.

**Resolution Steps**

Check application permissions and the size of the file to be downloaded.

## 2300025 Upload Failed

**Error Message**

Upload failed.

**Error Description**

Upload failed.

**Possible Causes**

The file is too large or there are network issues. For FTP, the server typically rejects the STOR command. The error buffer usually contains the server's explanation.

**Resolution Steps**

Check the file size and network conditions.

## 2300026 Failed to Open/Read Local Data from File/Application

**Error Message**

Failed to open/read local data from file/application.

**Error Description**

Failed to open/read local data from file/application.

**Possible Causes**

The application lacks file read permissions.

**Resolution Steps**

Check application permissions.

## 2300027 Out of Memory

**Error Message**

Out of memory.

**Error Description**

Out of memory.

**Possible Causes**

Insufficient memory.

**Resolution Steps**

Check system memory.

## 2300028 Operation Timeout

**Error Message**

Timeout was reached.

**Error Description**

Operation timeout.

**Possible Causes**

TCP connection timeout or read/write timeout.

**Resolution Steps**

Investigate network issues.

## 2300047 Maximum Redirects Reached

**Error Message**

Number of redirects hit maximum amount.

**Error Description**

Maximum number of redirects reached.

**Possible Causes**

Too many redirects.

**Resolution Steps**

Investigate the server implementation.

## 2300052 Empty Server Response

**Error Message**

Server returned nothing (no headers, no data).

**Error Description**

The server returned no content.

**Possible Causes**

May be related to the server implementation.

**Resolution Steps**

Investigate the server implementation.

## 2300055 Failed to Send Network Data

**Error Message**

Failed sending data to the peer.

**Error Description**

Failed to send data to the peer.

**Possible Causes**

Network issues.

**Resolution Steps**

Investigate the network.

## 2300056 Failed to Receive Network Data

**Error Message**

Failure when receiving data from the peer.

**Error Description**

Failed to receive data from the peer.

**Possible Causes**

Network issues.

**Resolution Steps**

Investigate network issues.

## 2300058 Local SSL Certificate Error

**Error Message**

Problem with the local SSL certificate.

**Error Description**

Local SSL certificate error.

**Possible Causes**

The SSL certificate format is incorrect.

**Resolution Steps**

Check the SSL certificate format.

## 2300059 Specified Cipher Unavailable

**Error Message**

Couldn't use specified SSL cipher.

**Error Description**

The specified cipher cannot be used.

**Possible Causes**

The encryption algorithm negotiated between client and server is not supported by the system.

**Resolution Steps**

Capture packets and analyze the negotiated algorithm.

## 2300060 Invalid Remote Server SSL Certificate or SSH Key

**Error Message**

SSL peer certificate or SSH remote key was not OK.

**Error Description**

The remote server's SSL certificate or SSH key is invalid.

**Possible Causes**

Failed to verify the server's identity, possibly due to an expired certificate.

**Resolution Steps**

Check the certificate validity.

## 2300061 Unrecognized or Malformed HTTP Encoding

**Error Message**

Unrecognized or bad HTTP Content or Transfer-Encoding.

**Error Description**

Unrecognized or malformed HTTP encoding.

**Possible Causes**

The HTTP encoding format is incorrect.

**Resolution Steps**

Investigate the server implementation. Currently, only gzip encoding is supported.## 2300063 Maximum File Size Exceeded

**Error Message**

Maximum file size exceeded.

**Error Description**

The file size exceeds the maximum limit.

**Possible Causes**

The downloaded file is too large.

**Resolution Steps**

Investigate server implementation.

## 2300070 Insufficient Server Disk Space

**Error Message**

Remote disk full or allocation exceeded.

**Error Description**

Insufficient server disk space.

**Possible Causes**

The server disk is full.

**Resolution Steps**

Check server disk space.

## 2300073 Server Indicates File Already Exists

**Error Message**

Remote file already exists.

**Error Description**

The server reports that the file already exists.

**Possible Causes**

During file upload, the server indicates the file already exists.

**Resolution Steps**

Investigate server configuration.

## 2300077 SSL CA Certificate Missing or Access Denied

**Error Message**

Problem with the SSL CA cert (path? access rights?).

**Error Description**

SSL CA certificate is missing or access is denied.

**Possible Causes**

The certificate does not exist or lacks proper access permissions.

**Resolution Steps**

Verify certificate existence and access permissions.

## 2300078 Requested File Not Found via URL

**Error Message**

Remote file not found.

**Error Description**

The file requested via URL does not exist.

**Possible Causes**

The file specified in the URL request cannot be found.

**Resolution Steps**

Check if the requested file exists at the specified URL.

## 2300094 Authentication Failure

**Error Message**

An authentication function returned an error.

**Error Description**

Authentication failed.

**Possible Causes**

The provided authentication credentials do not match server records.

**Resolution Steps**

Verify whether the authentication fields match server requirements.

## 2300999 Unknown Error

**Error Message**

Unknown Other Error.

**Error Description**

Unknown error occurred.

**Possible Causes**

Undetermined error condition.

**Resolution Steps**

Undetermined resolution steps.