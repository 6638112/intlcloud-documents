OpenSSL is a well-known open source cryptography toolkit for secure communications, and contains cryptographic algorithms, common passwords, and certificate packaging feature.

#### 1. Official Website of OpenSSL

Official download address: https://www.openssl.org/source/

#### 2. Installation Method on Windows

Windows version of the installation package is not provided on OpenSSL official website. You can choose tools provided by other open source platforms, for example: http://slproweb.com/products/Win32OpenSSL.html 
Taking this tool as an example, the installation steps and usage are as follows:
1. Download a 32-bit or 64-bit version, for example, Win64OpenSSL_Light-1_0_2h.exe, as shown below:
![](https://mccdn.qcloud.com/static/img/cc4da6cc001f66481967485fb6a035d6/openssl-1.png)
2. Set environment variables. If the tool is installed in C:\OpenSSL-Win64, copy `C:\OpenSSL-Win64\bin；` to Path
![](https://mccdn.qcloud.com/static/img/48f68528c408e6b7f83956fed009f3b7/openssl-2.png)
3. Open the command line program cmd (run as an administrator), enter the directory where 2_www.domain.com.key and 1_www.domain.com_cert.crt are stored, and run the command below
```
openssl pkcs12 -export -out www.domain.com.pfx -inkey 2_www.domain.com.key -in 1_www.domain.com_cert.crt
```
For example, the key and crt files are stored in D:\ and the operation is as follows:
![](https://mccdn.qcloud.com/static/img/2388c2fe32dc0bbe32347566fdfb6464/openssl-3.png)
Note: If Export Password is not required, press Enter directly without input.
4. After www.domain.com.pfx is generated in D:\, you can continue to complete the certificate installation in IIS Manager.
