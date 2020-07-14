In addition to [creating custom images](https://intl.cloud.tencent.com/document/product/213/4942), Tencent Cloud allows you to import images. You can import an image file of the system disk on a local or a different server into CVM custom images. You can use the imported image to create a CVM or reinstall the operating system (OS) for an existing CVM.

<span id="preparations for import"></span>
## Preparations

Prepare an image file that meets the import requirements.
- **Requirements for Linux images:**
<table>
<tr><th>Image Attribute</th><th>Requirements</th></tr>
<tr><td>OS</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, OpenSUSE, and SUSE</li><li>Both 32-bit and 64-bit OSs are supported.</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, and VMDK</li><li>Run <code>qemu-img info imageName | grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. Run <code>qemu-img info imageName | grep 'disk size'</code> to check the image size.</li><li>The image vsize cannot exceed 500 GB. Run <code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>size of an image in QCOW2 format is used upon check during import.</td></tr>
<tr><td>Network</td><td><ul><li>By default, Tencent Cloud provides the <code>eth0</code> network interface for the instance.</li><li>You can use the metadata service to query the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a>.</li></ul></td></tr>
<tr><td>Driver</td><td><ul><li>Virtio driver of the virtualization module KVM must be installed for an image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux System Check virtio Driver</a>.</li><li>We recommend installing cloud-init for the image. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12587">Install Cloud-Init on Linux</a>.</li><li>If cloud-init cannot be installed, configure the instance by referring to <a href="https://intl.cloud.tencent.com/document/product/213/12849">Forcibly Import Image</a>.</li></ul></td></tr>
<tr><td>Kernel</td><td>Native kernel is preferred for an image. Any modifications on the kernel may cause the import to fail.</td></tr>
</table>
- **Requirements for Windows images:**
<table>
<tr><th>Image Attribute</th><th>Requirements</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008, Windows Server 2012, and Windows Server 2016 related versions</li><li>Both 32-bit and 64-bit OSs are supported.</li></ul></td></tr>
<tr><td>Image format</td><td><ul><li>RAW, VHD, QCOW2, and VMDK</li><li>Run <code>qemu-img info imageName | grep 'file format'</code> to check the image format.</li></ul></td></tr>
<tr><td>File system type</td><td><ul><li>Only NTFS with MBR partition is supported.</li><li>GPT partition is not supported.</li><li>Logical Volume Manager (LVM) is not supported.</li></ul></td></tr>
<tr><td>Image size</td><td><ul><li>The actual image size cannot exceed 50 GB. Run <code>qemu-img info imageName | grep 'disk size'</code> to check the image size.</li><li>The image vsize cannot exceed 500 GB. Run <code>qemu-img info imageName | grep 'virtual size'</code> to check the image vsize.</li></ul><b>Note: </b>size of an image in QCOW2 format is used upon check during import.</td></tr>
<tr><td>Network</td><td><ul><li>By default, Tencent Cloud provides <code>local area connection</code> network interface for the instance. </li><li>You can use the metadata service to query the network configuration of the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4934">Instance Metadata</a>.</li></ul></td></tr>
<tr><td>Driver</td><td>Virtio driver of the virtualization module KVM must be installed for an image. By default, Virtio driver is not installed in Windows OS. You can install <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows Virtio Drivers</a> and then export the local image.</td></tr>
<tr><td>Others</td><td>Imported Windows images <b>do not support </b><a href="https://intl.cloud.tencent.com/document/product/213/2757">Windows license activation</a>.</td></tr>
</table>

## Directions

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)**.
 3. Select **Custom Image** and click **Import Image**.
 4. [Enable Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) and then [create bucket](/doc/product/436/6232). Upload the image file to the bucket and get the [image file URL](/doc/product/436/6260).
 5. Click **Next**.
 6. Complete the configurations and click **Import**.
 > Ensure the entered COS file URL is correct.
 >
You will be notified whether the import is successful via [internal message](https://console.cloud.tencent.com/message).

## Failed Imports

If you fail to import an image in the console, troubleshoot as follows:

### Notes

Make sure you have subscribed to product service notifications via [Message Subscription](https://console.cloud.tencent.com/messageCenter/messageConfig). This ensures you can receive internal messages, SMS messages, and emails about the cause of failure.
> If you do not subscribe to product service notifications, you will not receive the internal message about whether an import is successful.

### Troubleshooting

For more information on error messages and descriptions, see [Error Codes](# errorcode).

#### InvalidUrl: invalid COS URL

The InvalidUrl error indicates that an incorrect COS URL has been entered. The possible causes are:
* The image URL you entered is not a [Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) image URL.
* The access permission of the COS file is private read, but the signature has expired.
> COS URL with the signature can only be accessed once.
>
* A COS URL of another region has been entered.
> The image import service accesses the COS server in the local region through the private network.
>
* The user's image file has been deleted.
If you receive the error message about an invalid COS URL, troubleshoot based on the reasons above.

#### InvalidFormatSize: invalid format or size

The InvalidFormatSize error indicates that the format or size of an image to be imported does not meet the following requirements of Tencent Cloud:
* Supported image file formats are `qcow2`,` vhd`, `vmdk`, and` raw`.
* The size of an image file to be imported cannot exceed 50 GB (based on the size in qcow2 format).
* The size of the system disk to which the image is imported cannot exceed 500 GB.

If you receive an error message that the image format or size is invalid:
- Convert the image file into an appropriate format according to [Linux Image Creation](https://intl.cloud.tencent.com/document/product/213/17814), reduce its size to meet the requirements, and import again.
- Use [offline instance migration](https://console.cloud.tencent.com/csm/importOfflineCvm) to migrate the instance. This feature supports the migration of image files up to 500 GB.

#### VirtioNotInstall: Virtio driver not installed

The VirtioNotInstall error indicates that the image to be imported does not have Virtio driver installed. Tencent Cloud uses the KVM virtualization technology and requires users to install Virtio driver on the image to be imported. Except for a few customized Linux OSs, most Linux OSs have Virtio driver installed. In Windows OSs, users need to manually install the Virtio driver:
- For Linux image import, see [Linux System Check virtio Driver](https://intl.cloud.tencent.com/document/product/213/9929).
- For Windows image import, see [Windows Image Creation](https://intl.cloud.tencent.com/document/product/213/17815) to install the Virtio driver.

#### CloudInitNotInstalled: cloud-init program not installed

The CloudInitNotInstalled error indicates that the image to be imported does not have cloud-init installed. Tencent Cloud uses the open-source cloud-init software to initialize the CVM. If cloud-init is not installed, the CVM initialization will fail.
* For Linux image import, see [Install Cloud-Init on Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* For Windows image import, see [Installing Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
* After cloud-init or cloudbase-init is installed, replace the configuration file based on the corresponding document so the CVM can pull data from the correct data source upon startup.

#### PartitionNotPresent: partition information is lost

The PartitionNotPresent error indicates that the imported image is incomplete. Check whether the boot partition was included when the image was created.

#### RootPartitionNotFound: root partition is lost

The RootPartitionNotFound error indicates that the root partition cannot be detected in the image to be imported. Check the image file. The possible causes are:
* The installation package is uploaded.
* The data disk image is uploaded.
* The boot partition image is uploaded.
* An incorrect file is uploaded.

#### InternalError: unknown error

The InternalError error indicates that the cause of error has not yet been recorded. Contact the customer service and our technical personnel will help you resolve the issue as soon as possible.

<a id="errorcode"></a>
## Error Codes
 
| Error Code | Reason | Recommended Solution |
|-----|-----|-----|
| InvalidUrl | Invalid COS link. | Check whether the COS URL is the same as the imported image URL. |
| InvalidFormatSize | Format or size does not meet requirements. | Images must meet the `image format` and `image size` requirements in [Preparations](#PreparationsforImport). |
| VirtioNotInstall | Virtio driver not installed. | Install the Virtio driver in the image by referring to the `Driver` section in [Preparations](#PreparationsforImport). |
I PartitionNotPresent | Partition information not found. | Image is corrupted possibly due to incorrect image creation method. |
| CloudInitNotInstalled | Cloud-init software not installed. | Install cloud-init in the Linux image by referring to the `Driver` section in [Preparations](#PreparationsforImport). |
| RootPartitionNotFound | Root partition not found. | Image is corrupted possibly due to incorrect image creation method. |
| InternalError | Other errors. | Contact our customer service. |

