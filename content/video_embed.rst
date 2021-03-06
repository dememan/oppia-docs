Using Media Content in OppiaMobile Courses
======================================================

When a user installs a course containing media content (audio/video), the actual media aren't
included in the course download content. The reason for this is that media files 
tend to be very large and users on slow connections are unlikely to be able to 
download large media files.

If a course contains media files that aren't available on the users phone, on 
the app homepage a message will appear that some media content is missing.

Optimize your media
--------------------

Users viewing videos on a 4 or 5 inch screen generally don't need really high
quality as you may want to use if projecting the video. At Digital Campus, we
usually convert videos into .m4v format using Handbrake (https://handbrake.fr/
- an open source tool and works on most platforms)
   
How to embed media files in OppiaMobile courses
-------------------------------------------------

The method you can use to embed media in your course depends on the version of
the Moodle Oppia Export Block that you are using. 
   
Oppia Export Block v1.1.1 and below
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Upload the converted media to the OppiaMobile server (under the menu Upload -> Media), 
   this will then provide the embed code to put directly in the page content in Moodle.
   
Oppia Export Block v1.2.0 and above
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. On the page content you are editing, use the upload media button in the
   Moodle page text editor:
   
   .. image:: images/moodle-media-embed.png
   
   From the pop-up window, select the 'Video' tab, then click the 'Browse
   repositories' button:
   
   .. image:: images/insert-media.png
   
   Then select 'Upload a file':
   
	.. image:: images/upload-file.png
	
	Choose the file to upload and click 'Upload this file'
	
	To add a ``poster/thumbnail`` image to your video (this is the image that 
	users will see in the Oppia app and will click on to start the video),
	select 'Display Options' and upload a poster/thumbnail of the video:
	
	.. image:: images/add-poster.png
	
	Then click on the 'Insert Media' button
	
#. The export process will automatically handle uploading the media to the Oppia
   server

.. note::
	
	If you don't add a ``poster/thumbnail`` when you upload the video, on 
	exporting to Oppia you will see a warning message and in the app just a text
	link to 'Play video' will appear, rather than an image.
	
How can users get the media files
----------------------------------

There are two options for getting the media content onto users phones:

#. Download the media files directly onto the users SD card. This is most 
   likely the best option for projects which are providing phones to users as 
   the video files can be pre-loaded
#. Download via the app. When the app flags up that a video file is missing, 
   then the user can download directly to their phone. This is only likely to be
   feasible to users who are connected to wifi. So by default users will only be 
   able to download video files directly if they are connected to a wifi network. 
   This can be overridden in the app settings to allow downloading of video 
   files by allowing downloading using cellular network.
   
   
Manually creating the embed code (deprecated from v1.2.0 onwards)
-------------------------------------------------------------------

Should you really want to, you can create the media embed code by hand:

#. Generate the md5 checksum for your media. All operating systems will allow 
   you to generate an md5 checksum of a file. The md5 is essentially a unique 
   code to identify a file and it's contents. We use this for the media, so 
   when a user download the media on their phone the app can verify they have 
   the complete media (and no broken/partial downloads) and the correct media.
#. Now you have md5 and the file uploaded to a server you can embed your media 
   into your page on Moodle using the following code:
   
   .. code-block:: text
   		
   		[[media object='{“filename”:”ghmp-basic-skills-20121001.m4v”,
   					”download_url”:”http://downloads.digital-campus.org/media/pnc/ghmp-basic-skills-20121001.m4v”,
   					”digest”:”3ec4d8ab03c3c6bd66b3805f0b11225b”}’]]IMAGE/TEXT HERE[[/media]]
   
   Just update the filename, download_url and digest (md5) to match your video 
   file details.
#. You can replace the ``IMAGE/TEXT HERE`` with either some text or a screenshot
   of you video. When your course is exported from Moodle, the export script 
   will use the supplied information to ensure the user downloads the correct 
   video.
#. You optionally supply a filesize (in bytes) and length (in seconds) as 
   follows:

   .. code-block:: text
	
	   [[media object='{“filename”:”ghmp-basic-skills-20121001.m4v”,
						”download_url”:”http://downloads.digital-campus.org/media/pnc/ghmp-basic-skills-20121001.m4v”,
						”digest”:”3ec4d8ab03c3c6bd66b3805f0b11225b”, 
						“filesize”:312345657, 
						“length”:360}’]]IMAGE/TEXT HERE[[/media]]
	
   Adding a filesize will inform the user how large the file is before they try
   to download and the length will be used to determine whether a user has 
   watched the whole video (or not). 

