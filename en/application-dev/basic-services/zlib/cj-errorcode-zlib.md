# zlib Error Codes

> **Note:**
>
> This topic describes only module-specific error codes. For details about universal error codes, see the [Universal Error Code Documentation](../../reference/cj-errorcode-universal.md).

## 17800002 Incorrect File or Access Mode

**Error Message**

No such file or access mode error.

**Error Description**

This error code is reported when the file path, file descriptor, or file access mode passed in the **gzopen** or **gzdopen** API is incorrect.

**Possible Causes**

1. When the **gzopen** API is called, the file path or file access mode passed in is incorrect.
2. When the **gzdopen** API is called, the file descriptor or file access mode passed in is incorrect.

**Resolution Steps**

1. Check whether the gz file path or file descriptor is correct. If a new gz file is to be created, make sure the file access mode is a compression mode (such as w or wb).
2. Check whether the file access mode is "w", "wb", "r", "rb", "a", "ab", or the like.

## 17800004 Compression or Decompression Stream Error

**Error Message**

Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure.

**Error Description**

This error code is reported when the compression or decompression stream is abnormal during the invocation of APIs such as **deflate** or **inflate**.

**Possible Causes**

1. When APIs such as **deflate** or **inflate** are called, the compression or decompression stream is not initialized by using **deflateInit** or **inflateInit** in advance.
2. When APIs such as **gzsetparams**, **gzclose**, or **gzflush** are called, the flush mode passed in is incorrect, or the file access mode passed in the gz file opening API is incorrect before the invocation.

**Resolution Steps**

1. Before calling APIs such as **deflate** or **inflate**, initialize the compression or decompression stream by using **deflateInit** or **inflateInit**.
2. Check whether the gz file opening API is not called or fails to be called before the invocation.
3. Check whether the access mode passed in the gz file opening API matches the API to be called. For example, **gzprintf** is a compression API. Therefore, the access mode passed in the gz file opening API must be a compression mode (such as w or wb).
4. Check whether the enum parameters passed in are correct.

## 17800005 Incorrect Input Data

**Error Message**

The input data is incorrect. For example, the data does not conform to the zlib compression format, the compressed data is corrupted, or the data is not compressed.

**Error Description**

This error code is reported when the data passed in APIs such as **uncompress** is incorrect.

**Possible Causes**

When the **uncompress** API is called, the data is not compressed by using **compress** in advance.

**Resolution Steps**

Compress the data by using **compress** before decompressing it by using **uncompress**.

## 17800006 Memory Allocation Failure

**Error Message**

Memory allocation failed.

**Error Description**

This error code is reported when memory allocation fails during the invocation of the **gzclose** API.

**Possible Causes**

Before the **gzclose** API is called, the **gzsetparams** API is called with an incorrect compression level or compression strategy.

**Resolution Steps**

Check the invocation of the **gzsetparams** API, and pass in the correct compression level and compression strategy.

## 17800007 Incorrect Buffer

**Error Message**

The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data.

**Error Description**

This error code is reported when the buffer passed in APIs such as **compress**, **compress2**, or **uncompress** is incorrect.

**Possible Causes**

1. When the **uncompress** API is called, the size of the input buffer passed in is greater than that of the output buffer after decompression.
2. When the **compress** or **compress2** API is called, the size of the input buffer passed in is greater than that of the output buffer after compression.
3. When APIs such as **compress**, **compress2**, or **uncompress** are called, the size of the buffer passed in is 0.

**Resolution Steps**

Increase the size of the corresponding buffer.

## 17800009 Internal Structure Error

**Error Message**

Internal structure error.

**Error Description**

This error code is reported when the parameters passed in APIs such as **gzwrite** or **gzread** are incorrect, or the file access mode passed in the gz file opening API is incorrect before the invocation.

**Possible Causes**

1. The gz file opening API is not called or fails to be called before the invocation.
2. The file access mode passed in the gz file opening API is incorrect before the invocation.
3. When the **gzwrite** API is called, the length of uncompressed bytes passed in is 0.
4. When the **gzgets** API is called, an empty ArrayBuffer is passed in.
5. When the **gzread** API is called, the gz file is empty.

**Resolution Steps**

1. Check whether the gz file opening API is not called or fails to be called before the invocation.
2. Check whether the access mode passed in the gz file opening API matches the API to be called. For example, **gzread** is a decompression API. Therefore, the access mode passed in the gz file opening API must be a decompression mode (such as r or rb).
3. Check whether the parameters passed in are correct.

## 900001 Invalid Source File

**Error Message**

The input source file is invalid.

**Error Description**

This error code is reported when the source file passed in the **compressFile** or **decompressFile** API is invalid.

**Possible Causes**

1. The source file path passed in is empty, contains a relative path, or is not a valid application sandbox path.
2. The source file passed in does not exist, or the application does not have the read permission on the source file.
3. When the **decompressFile** API is called, the source file cannot be opened.

**Resolution Steps**

1. Check the source file path.

   Make sure the path is not empty, does not contain a relative path (such as "../"), and is under the correct application sandbox path.

2. Check whether the source file exists and whether the application has the read permission on the source file.

3. When the **decompressFile** API is called, check whether the source file can be opened, and make sure the file name extension is .zip.

## 900002 Invalid Destination File

**Error Message**

The input destination file is invalid.

**Error Description**

This error code is reported when the destination file passed in the **compressFile** or **decompressFile** API is invalid.

**Possible Causes**

1. The destination path passed in is empty, contains a relative path, or is not a valid application sandbox path.
2. When the **decompressFile** API is called, the destination path passed in does not exist or is not a directory.
3. The application does not have the write permission on the destination directory.
4. The output directory cannot be created during decompression, or the destination file cannot be created or opened.

**Resolution Steps**

1. Check the destination path.

   Make sure the path is not empty, does not contain a relative path (such as "../"), and is under the correct application sandbox path.

2. Before calling the **decompressFile** API, check whether the destination path is an existing directory. If the directory does not exist, create the directory first.

3. Check whether the application has the write permission on the destination directory.

4. Check whether there are abnormal entries in the destination directory that prevent the creation of a directory or file with the same name, and make sure the destination directory has sufficient available storage space.

## 900003 Source File in Incorrect Format or Damaged

**Error Message**

The input source file is not in ZIP format or is damaged.

**Error Description**

This error code is reported when the compression format of the source file passed in the **decompressFile** API is incorrect or the source file is damaged.

**Possible Causes**

1. The source file passed in is not in ZIP format, or the file is incomplete or damaged.
2. The entry path in the ZIP file contains a relative path (such as "../").
3. The entry information or entry data in the ZIP file is damaged, causing the entry to fail to be read or decompressed.

**Resolution Steps**

1. Check whether the source file is a valid and complete ZIP file.

   If the source file is downloaded over the network, make sure the file is downloaded before calling the **decompressFile** API. If the file is damaged, generate or obtain the ZIP file again.

2. Check the entry paths in the ZIP file, and make sure the paths do not contain relative paths (such as "../"). If such entries exist, remove them and generate the ZIP file again.

3. Check whether each entry in the ZIP file can be properly read and decompressed. If an entry is damaged, generate or obtain the ZIP file again.
