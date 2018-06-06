# Rho.Camera
				This Property shall return one among the values mentioned in constant section which starts with CAMERA_TYPE_...
				
				In UWP, only filename can be changed, by default the path shall be under picture=>CameraRoll
				This Property shall accept/return one among the values mentioned in constant section which starts with COMPRESSION_FORMAT_...
				
				This Property shall accept/return one among the values mentioned in constant section which starts with OUTPUT_FORMAT_...
				This Property shall accept/return one among the values mentioned in constant section which starts with COLOR_MODEL_...
				This Property shall accept/return one among the values mentioned in constant section which starts with FLASH_...
				This Property shall accept/return one among the values mentioned in constant section which starts with AIM_...
                  Start the camera application to take a picture. The user can capture the displayed image by interacting with the resident camera app. In Windows, this method always shows the preview in full screen and user can use the native button to capture the image.
                  When you use 'outputFormat' is 'image' captured image will be saved into file and you should control this file by self - remove it if you do not use it anymore etc.
                  On UWP,wm when 'outputFormat' is 'image' then imageUri/image_uri shall have only Image name with \ sign, on UWP ImageName shall be suffixed by DTF when 'outputFormat' is 'image'
                  > Note: To display an image, it is recommended that you use the full path to the image instead of a relative path. To do this, you can use the [`expandDatabaseBlobFilePath`](Application#mexpandDatabaseBlobFilePath) method of the [Application module](Application) as such:

                  ##### Ruby
                  :::ruby
                  Rho::RhoApplication.expandDatabaseBlobFilePath(x.image_uri)

                  ##### JavaScript
                  :::js
                  Rho.RhoApplication.expandDatabaseBlobFilePath(x.image_uri)
                