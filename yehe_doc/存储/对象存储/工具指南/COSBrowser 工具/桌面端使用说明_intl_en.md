## Download and installation

#### Download

| OS | OS Requirement | Download Link |
| :------- | :---------------------------------------------------------- | :----------------------------------------------------------- |
| Windows | Windows 7 32/64-bit or above, Windows Server 2008 R2 64-bit or above | [Windows](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe) |
| macOS | macOS 10.13 or above | [macOS](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest.dmg) |
| Linux | Includes GUI and supports the [AppImage](https://appimage.org/) format | [Linux](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-latest-linux.zip) |
| Website version | Browsers such as Chrome, FireFox, Safari, and IE10+ | [Web](https://cosbrowser.cloud.tencent.com/web) |

#### Installation

The COSBrowser installation package is an executable file. You can double-click the downloaded file and then install as prompted.

> !To launch the client running CentOS, you need to run `./cosbrowser.AppImage --no-sandbox` in the terminal.

## Login

You can log in to COSBrowser Desktop Edition with your Tencent Cloud API key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi) in the CAM console. After you logged in successfully, the key will be saved in **Historical Key** for future use. The login page is as shown below:

> !Logging in to COSBrowser with a project key is not supported.

<img src="https://main.qcloudimg.com/raw/5fcb01823ae8220e035e86bfd12f047c.png" width="90%">


## Basic Features

<span id="createordelete"></span>

#### 1. Creating/Deleting bucket

| Feature | Description | Directions |
| ---------- | -------------------------------------- | ------------------------------------------------------------ |
| Creating bucket | You can create a bucket directly via the client | 1. In the bucket list, click **Add Bucket** in the upper-left corner<br />2. Enter the bucket name correctly, and select your region and access permissions<br />3. Click **OK**|
| Deleting bucket | Before you delete a bucket, ensure that all data in the bucket has been cleared | 1. In the bucket list, click **Delete** on the right of the selected bucket <br />2. Click **OK**|

<span id="viewbucket"></span>

#### 2. Viewing bucket details

You can view bucket details by clicking **Details** on the right of the bucket list. Details include bucket name, region, access permissions, and versioning status.


<span id="count"></span>

#### 3. Viewing statistics

You can click **…** > **Statistics** to view the bucket statistics, including the storage usage and the number of objects.

<span id="acl"></span>

#### 4. Managing permissions

You can use COSBrowser to manage permissions for buckets and objects.

- Bucket permissions: Click **Permission Management** on the right of the bucket list.
- Object permissions: Click **Permission Management** on the right of the object.

>?For more information about COS permissions, please see [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).

<span id="version"></span>

#### 5. Setting versioning

You can use COSBrowser to enable/disable versioning for a bucket.

To configure versioning, click **Versioning** on the right of the bucket list.

>?For more information about versioning, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

<span id="addaccess"></span>

#### 6. Adding an access path

If you log in with a sub-account that does not have permission to access the bucket list, you can initiate an access via **Add Access Path** in the following two ways:
(1) Add an access path directly on the login page and select the corresponding bucket region. Once you log in, you can manage your resources.
<img src="https://main.qcloudimg.com/raw/5d80a51cd9b9a9c4d14fec9d4275a41d.png" width="90%">
(2) Log in with your sub-account, click **Add Path** in the upper-left corner of the bucket list page, and enter a specified path to enter the bucket and manage its resources.
<img src="https://main.qcloudimg.com/raw/3e66b023a607ea11ae224d2ec3eb3d4c.png" width="60%">

<span id="upload"></span>

#### 7. Uploading file/folder

<table>
   <tr>
      <th>Upload Feature</th>
      <th>Notes</th>
      <th>Directions</th>
   </tr>
   <tr>
      <td>Uploading files</td>
      <td >COSBrowser allows you to upload a single file or multiple files in batches in different ways.</td>
      <td nowrap="nowrap">You can upload files in the following ways. In the specified bucket or path:<br>1. Click **Upload Files** to upload files directly. <br>2. Right-click in the blank space of the file list and select **Upload Files** to upload files. <br>3. Drag a file to the file list pane.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Uploading a folder and the files contained</td>
      <td>If the name of the file/folder to upload already exists in the bucket or path, the old file/folder will be overwritten by default.</td>
      <td nowrap="nowrap">You can upload a folder in the following ways. In the specified bucket or path:<br>1. Click **Upload Folder** to upload a folder directly. <br>2. Right-click in the blank space of the file list and select **Upload Folder** to upload a folder. <br>3. Drag a folder to the file list pane.</td>
   </tr>
   <tr>
      <td>Incremental upload</td>
      <td>Incremental upload compares the files to upload with existing files in the bucket before the upload. An existing file with the same name in the bucket will be skipped.</td>
      <td>You can perform the following 2 steps to use incremental upload. In the specified bucket or path:<br>1. Upload as you do with a folder and click **Next**.<br>2. In **Storage method**, select **Skip**. Then, click **Upload** to begin the incremental upload.</td>
   </tr>
</table>



<span id="download"></span>

#### 8. Downloading file/folder

<table>
   <tr>
      <th>Download Feature</th>
      <th>Notes</th>
      <th>Directions</th>
   </tr>
   <tr>
      <td>Downloading files</td>
      <td>COSBrowser allows you to download a single file or multiple files in batches in different ways.</td>
      <td nowrap="nowrap">You can download a file in the following ways:<br>1. Select the desired file and click **Download** in the UI.<br>2. Right-click the file and select **Download**.<br>3. Drag the file to the local file system.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Downloading a folder and files contained</td>
      <td>If the name of the file/folder to download already exists in the local file system, it will be renamed by default.</td>
      <td>You can download a folder and the files contained in the following ways:<br>1. Select the desired folder and click **Download** in the UI.<br>2. Right-click the folder and select **Download**.<br>3. Drag a folder to the local file system.</td>
   </tr>
   <tr>
      <td>Incremental download</td>
      <td>Incremental download compares the files to download with local files before the download. An existing file with the same name will be skipped.</td>
      <td>You can perform the following 3 steps to use incremental download:<br>1. Select the desired file/folder, move the mouse to **More**, and a drop-down list will appear.<br>2. Click **Advanced Download** in the drop-down list and select **Skip** in the dialog box.<br>3. Click **Download Now** to incrementally download new files/folders.</td>
   </tr>
</table>

<span id="delete"></span>

#### 9. Deleting file/folder	

To delete a file/folder, select the file/folder to delete and click **Delete** in **More** at the top of the UI, or right-click it and select **Delete**. You can delete multiple files/folders in batches.

<span id="synchronization"></span>

#### 10. Synchronizing file

The file synchronization feature allows you to upload specified files in your local folders to a bucket in real time. Detailed directions are as follows:

(1) Click **Sync** in the upper right of the UI.
(2) Specify a local folder and bucket directory in the dialog box.
(3) Click **Start Sync** to enable file synchronization.
(4) View synchronization history logs in **Sync Logs** tab.
<img src="https://main.qcloudimg.com/raw/283c7f9ee254b08561084ece22e2ada2.png" width="90%" />

> !
> - Synchronization means that when the file is uploaded, the system automatically identifies whether the same file exists in the bucket. Only files that do not exist in the bucket are synchronously uploaded.
> - Currently, only synchronizing local files to the bucket is supported. Reverse operation is not supported.
> - Both manual and automatic synchronization are supported.

<span id="copy"></span>

#### 11. Copying and pasting file

To copy a file/folder, select the desired file/folder in the specified bucket/path and click **Copy** in **More** at the top of the UI. Alternatively, you can right-click it and select **Copy**. After the file/folder is successfully copied, you can paste it to **another bucket or path**. You can copy and paste multiple files/folders in batches.

> !If the name of the file/folder to paste already exists in the destination path, the old file/folder will be overwritten by default.

<span id="rename"></span>

#### 12. Renaming file

Select a file you want to rename, right-click, and select **Rename**. Alternatively, you can click **Rename** in **More Actions** on the right of the file. Then, enter your file name, and click **OK**.

> ?Folders cannot be renamed.

<span id="newfolder"></span>

#### 13. Creating folder

To create a folder in the specified bucket or path, click **Create Folder** in the UI, or right-click in the UI and select **Create Folder**, enter the folder name, and click OK.

> !
> - The folder name can contain up to 255 characters, including digits, letters, and visible characters.
> - The folder name cannot contain special characters such as `\ / : * ? " | < >`.
> - `..` cannot be used as the folder name.
> - The folder cannot be renamed.

<span id="view"></span>

#### 14. Viewing file details

To view the details of a file, click its filename or right-click it and select **Detail**. File details include filename, file size, modification time, access permission, storage class, ETag, headers, endpoint, object location, and an option to create a temporary object URL.

<img src="https://main.qcloudimg.com/raw/9b5b80c75be055240afcbe49cca6ff42.png" width="70%">


<span id="generatelinks"></span>

#### 15. Generating file URL

Each file stored in COS can be accessed through a specific URL. If a file is private-read, you can request a temporary signature to generate a temporary access URL with a certain validity period.

You can generate a file URL in the following ways:

- In the list view, click the Share icon on the right of the object to generate a URL and copy it. If the file is public-read, the URL will not carry a signature and be valid permanently. If the file is private-read, the URL will carry a signature and be valid for 2 hours.
- Right-click a file and select **Copy Link** to generate a URL and copy it. If the file is public-read, the URL will not carry a signature and be valid permanently. If the file is private-read, the URL will carry a signature and be valid for 2 hours.
- On the file detail page, click **Create link with expires** to set the temporary URL, URL type, and validity period for the specified endpoint (available only when a CDN acceleration endpoint is enabled).

 <img src="https://main.qcloudimg.com/raw/18f72dceccdaeaf9171acf0b08917107.png" width="60%">

<span id="preview"></span>

#### 16. Previewing file

COSBrowser allows you to preview media files, including images, videos, and audio. To preview a media file, double-click it or right-click it and select **Preview** or **Playback** in the context menu. On the file preview or playback screen, you can click:

- **Copy Link** to generate a file access URL and copy it.
- **Download** to download the file to the local file system. If a file with the same name already exists in the local file system, it will be overwritten by default.
- **View on Mobile** to generate a QR code for the file, which can be scanned on a mobile phone for direct view.

> !
> - Preview is available for images in most formats, .mp4 and .webm videos, and .mp3. and .wav audios.
> - Please note that file preview will incur downstream traffic.

![](https://main.qcloudimg.com/raw/b5b58260b55344aaef8028fa2df27fdb.png)

<span id="searchfile"></span>

#### 17. Searching for file

To search for a file, enter the filename in the search box at the top right of the bucket. COSBrowser supports prefix search and fuzzy search.

<span id="searchbuckete"></span>

#### 18. Searching for bucket

To quickly locate a bucket, enter the bucket name in the search box above the bucket list on the left.

<span id="viewfiles"></span>

#### 19. Viewing historical versions or incomplete multipart uploads

- If versioning is enabled for your bucket, you can click **View** > **Multiversion list** above the file list to view the historical versions. Prefix search and clearing all historical versions (retaining the latest version only) are supported.
<img src="https://main.qcloudimg.com/raw/5fb6a486881f0aeef1682c9944262698.png" width="80%">

- If you pause or cancel an ongoing upload, incomplete multipart uploads may be generated. You can click **View** > **Incomplete Multipart Uploads** above the file list to view them. Prefix search and clearing all incomplete multipart uploads are supported.
![](https://main.qcloudimg.com/raw/17b7a096e0e4388f3fabc82f6a0ef7b2.png)

<span id="sets"></span>

## Settings

<table>
   <tr>
      <th nowrap="nowrap">System Feature</th>
      <th>Notes</th>
      <th>Directions</th>
   </tr>
   <tr>
      <td>Setting up proxy</td>
      <td >COSBrowser uses the system-configured proxy to connect to the Internet. Please make sure that your proxy is set up properly or disable the proxy configuration if it fails to connect to the Internet.</td>
      <td nowrap="nowrap">1. Select **Settings** > **Proxy**.<br>2. Set up a proxy to connect to the Internet.</td>
   </tr>
   <tr>
      <td>Setting the number of concurrent transfers</td>
      <td>COSBrowser supports uploading/downloading multiple files in batches.</td>
      <td>1. Select **Settings** > **Download/Upload**. <br>2. Set the number of concurrent transfers, which is 5 by default.</td>
   </tr>
   <tr>
      <td>Setting the number of parts to transfer</td>
      <td>COSBrowser supports uploading/downloading a file in multiple parts. When the file to be transferred exceeds a certain size, multipart transfer will be performed by default.</td>
      <td>1. Select **Setting** > **Download/Upload**.<br>2. Set the number of concurrent parts to be transferred, which is 5 by default.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Setting the number of retries upon transfer failure</td>
      <td>COSBrowser will retry failed tasks by default when transferring files.</td>
      <td>1. Select **Settings** > **Download/Upload**.<br>2. Set the number of retries upon transfer failure, which is 5 by default.</td>
   </tr>
   <tr>
      <td>Setting upload check</td>
      <td>COSBrowser supports checking files online after upload to verify whether their size and status are correct.</td>
      <td>1. Select **Settings** > **Upload**.<br>2. Select "Upload Check".</td>
   </tr>
   <tr>
      <td>Limiting single-thread speed</td>
      <td>COSBrowser supports limiting the upload and download speeds for a single thread. Total upload (download) speed limit = Single-thread upload (download) speed limit x Number of concurrent files x Number of concurrent parts</td>
      <td>1. Select **Settings** > **Upload/Download**.<br>2. Set the single-thread upload/download speed limit, in MB/s.</td>
   </tr>
   <tr>
      <td>Viewing local log</td>
      <td>COSBrowser will record all the performed operations in the `cosbrowser.log` local file.</td>
      <td nowrap="nowrap">1. Select **Settings** > **About**.<br>2. Click **Local Log** and the system will open the directory where the local log is stored.</td>
   </tr>
</table>



