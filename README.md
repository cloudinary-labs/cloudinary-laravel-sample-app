## Laravel Cloudinary Sample App

## Disclaimer

> _This software/code provided under Cloudinary Labs is an unsupported pre-production prototype undergoing further development and provided on an “AS IS” basis without warranty of any kind, express or implied, including, but not limited to, the implied warranties of merchantability and fitness for a particular purpose are disclaimed. Furthermore, Cloudinary is not under any obligation to provide a commercial version of the software.</br> </br> Your use of the Software/code is at your sole risk and Cloudinary will not be liable for any direct, indirect, incidental, special, exemplary, consequential or similar damages (including, but not limited to, procurement of substitute goods or services; loss of use, data, or profits; or business interruption) however caused and on any theory of liability, whether in contract, strict liability, or tort (including negligence or otherwise) arising in any way out of the use of the Software, even if advised of the possibility of such damage.</br> </br> You should refrain from uploading any confidential or personally identifiable information to the Software. All rights to and in the Software are and will remain at all times, owned by, or licensed to Cloudinary._

## Getting started

- Clone this repo
- Run `composer install`
- Set your environment variable in your `.env` file: `CLOUDINARY_URL=xxxxxxxxxxxx`
- Run `php artisan serve`
- Access the `/upload` route to test uploads
- Access the `/` route to test the image and video component

## Laravel Controller in Use

- app/Http/Controllers/FileUploadController.php

## Blade Component in use for video and image tag

- resources/views/welcome.blade.php

## View for upload

- resources/views/upload.blade.php



```php

/**
*  Using the Cloudinary Facade
*/

// Upload an Image File to Cloudinary with One line of Code
$uploadedFileUrl = Cloudinary::upload($request->file('file')->getRealPath())->getSecurePath();

// Upload an Video File to Cloudinary with One line of Code
$uploadedFileUrl = Cloudinary::uploadVideo($request->file('file')->getRealPath())->getSecurePath();

// Upload any File to Cloudinary with One line of Code
$uploadedFileUrl = Cloudinary::uploadFile($request->file('file')->getRealPath())->getSecurePath();

/**
 *  This package also exposes a helper function you can use if you are not a fan of Facades
 *  Shorter, expressive, fluent using the
 *  cloudinary() function
 */

// Upload an Image File to Cloudinary with One line of Code
$uploadedFileUrl = cloudinary()->upload($request->file('file')->getRealPath())->getSecurePath();

// Upload an Video File to Cloudinary with One line of Code
$uploadedFileUrl = cloudinary()->uploadVideo($request->file('file')->getRealPath())->getSecurePath();

// Upload any File to Cloudinary with One line of Code
$uploadedFileUrl = cloudinary()->uploadFile($request->file('file')->getRealPath())->getSecurePath();

/**
 *  You can also skip the Cloudinary Facade or helper method and laravel-ize your uploads by simply calling the
 *  laravel store() method and pass 'cloudinary' as the second option which indicates the disk name
 *  or just use the storeOnCloudinary() method on the file itself
 */

// Store the uploaded file in the "anaconda" directory on Cloudinary
$result = $request->file('file')->store('anaconda', 'cloudinary');

// Store the uploaded file on Cloudinary
$result = $request->file('file')->storeOnCloudinary();

// Store the uploaded file on Cloudinary
$result = $request->file->storeOnCloudinary();

// Store the uploaded file in the "lambogini" directory on Cloudinary
$result = $request->file->storeOnCloudinary('lambogini');

// Store the uploaded file in the "lambogini" directory on Cloudinary with the filename "prosper"
$result = $request->file->storeOnCloudinaryAs('lambogini', 'prosper');


$result->getPath(); // Get the url of the uploaded file; http
$result->getSecurePath(); // Get the url of the uploaded file; https
$result->getSize(); // Get the size of the uploaded file in bytes
$result->getReadableSize(); // Get the size of the uploaded file in bytes, megabytes, gigabytes or terabytes. E.g 1.8 MB
$result->getFileType(); // Get the type of the uploaded file
$result->getFileName(); // Get the file name of the uploaded file
$result->getOriginalFileName(); // Get the file name of the file before it was uploaded to Cloudinary
$result->getPublicId(); // Get the public_id of the uploaded file
$result->getExtension(); // Get the extension of the uploaded file
$result->getWidth(); // Get the width of the uploaded file
$result->getHeight(); // Get the height of the uploaded file
$result->getTimeUploaded(); // Get the time the file was uploaded
```

**Attach Files** to Laravel **Eloquent Models**:

```php
/**
 *  How to attach a file to a Model by model creation
 */
$page = Page::create($this->request->input());
$page->attachMedia($file);   // Example of $file is $request->file('file');

/**
 *  How to attach a file to a Model by retreiving model records
 */
$page = Page::find(2);
$page->attachMedia($file);  // Example of $file is $request->file('file');

/**
 *  How to retrieve files that were attached to a Model
 */
$filesBelongingToSecondPage = Page::find(2)->fetchAllMedia();

/**
 *  How to retrieve the first file that was attached to a Model
 */
$fileBelongingToSecondPage = Page::find(2)->fetchFirstMedia();

/**
 *  How to retrieve the last file that was attached to a Model
 */
$fileBelongingToSecondPage = Page::find(2)->fetchLastMedia();

/**
 *  How to replace/update files attached to a Model
 */
$page = Page::find(2);
$page->updateMedia($file);  // Example of $file is $request->file('file');

/**
*  How to detach a file from a Model
*/
$page = Page::find(2);
$page->detachMedia($file)  // Example of $file is $request->file('file');
```

**Upload Files Via An Upload Widget**:

Use the `x-cld-upload-button` Blade component that ships with this Package like so:
```
<!DOCTYPE html>
<html>
    <head>
        ...
        @cloudinaryJS
    </head>
    <body>
        <x-cld-upload-button>
            Upload Files
        </x-cld-upload-button>


        <x-cld-image public-id='xxxxxxx'></x-cld-image>

        <x-cld-video public-id='xxxxxxx'></x-cld-video>


    </body>
</html>
````
