# emotioncreators-upload-server
I company emotion workshop upload and download server

<br />
<h1> Description </h1>
I tried to do this because the server of the original game blocked the domestic IP. <br />
The function of these codes is to serve the emotioncreators of Illusion as an alternative upload and download server. <br />
These codes have not been tested, so there may be bugs. <br />
I am also new to PHP, and I wrote this while doing Google, so it may not be able to provide code help.
<br />
<br />
<br />
<h1> Use note </h1>
If you want to use it, please set upload_max_filesize, post_max_size, memory_limit in php.ini. <br />
Set to a reasonable size that allows uploading files. <br />
<br />
And max_execution_time, max_input_time. <br />
Set a maximum time for accepting uploads and downloads to avoid upload or download failure. <br /> <br />
When it is officially set up, you need to set the close_error_report of data / config.ini to 1, to avoid returning strange things.
<br />
<br/>
The mysql sql file is in the sql folder. <br />
data / config.ini can modify the mysql connection configuration. <br /> <br />

The thumbnail in config.ini starts with the thumbnail size. <br />
image_base64 stores the image in base64 encoding. <br />
close_error_report is to close php's built-in error. If it is turned on, it may cause errors during actual use of the game. <br />
version is the version of the game. <br />
<br />
<br />
<br />

<h1> About modifying game connections </h1>
Game connection address, in emotioncreators / DefaultData / url <br />
The .dat inside is the connection address, but all are encrypted. <br /> <br />

Here is the encryption code. <br /> <br />
The encryption and decryption tool has been released in the forum post. The following is the C # code for encryption and decryption. <br />

EncryptAES (bytes, "eromake", "phpaddress") <br />
DecryptAES (bytes, "eromake", "phpaddress"); <br />

<pre>
<code>
public static byte [] EncryptAES (byte [] srcData, string pw = "illusion", string salt = "unityunity")
{
RijndaelManaged rijndaelManaged = new RijndaelManaged ();
rijndaelManaged.KeySize = 128;
rijndaelManaged.BlockSize = 128;
byte [] bytes = Encoding.UTF8.GetBytes (salt);
Rfc2898DeriveBytes rfc2898DeriveBytes = new Rfc2898DeriveBytes (pw, bytes);
rfc2898DeriveBytes.IterationCount = 1000;
rijndaelManaged.Key = rfc2898DeriveBytes.GetBytes (rijndaelManaged.KeySize / 8);
rijndaelManaged.IV = rfc2898DeriveBytes.GetBytes (rijndaelManaged.BlockSize / 8);
ICryptoTransform cryptoTransform = rijndaelManaged.CreateEncryptor ();
byte [] result = cryptoTransform.TransformFinalBlock (srcData, 0, srcData.Length);
cryptoTransform.Dispose ();
return result;
}

public static byte [] DecryptAES (byte [] srcData, string pw = "illusion", string salt = "unityunity")
{
RijndaelManaged rijndaelManaged = new RijndaelManaged ();
rijndaelManaged.KeySize = 128;
rijndaelManaged.BlockSize = 128;
byte [] bytes = Encoding.UTF8.GetBytes (salt);
Rfc2898DeriveBytes rfc2898DeriveBytes = new Rfc2898DeriveBytes (pw, bytes);
rfc2898DeriveBytes.IterationCount = 1000;
rijndaelManaged.Key = rfc2898DeriveBytes.GetBytes (rijndaelManaged.KeySize / 8);
rijndaelManaged.IV = rfc2898DeriveBytes.GetBytes (rijndaelManaged.BlockSize / 8);
ICryptoTransform cryptoTransform = rijndaelManaged.CreateDecryptor ();
byte [] result = cryptoTransform.TransformFinalBlock (srcData, 0, srcData.Length);
cryptoTransform.Dispose ();
return result;
}
</ code>
</ pre>
