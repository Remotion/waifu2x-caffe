waifu2x-caffe (for Windows)
----------

 Author: lltcggie

This software, image conversion software "[waifu2x] (https://github.com/nagadomi/waifu2x)" only the conversion function of,
[Caffe] rewrite using the (http://caffe.berkeleyvision.org/), is software that was built into Windows.
Can also will be converted by the CPU, but when using the CUDA (or cuDNN) can be converted faster than CPU.

GUI supports English and Japanese and Simplified Chinese and Traditional Chinese and Korean and Turkish.

Software downloads are available in the section "Downloads" on the [This releases page] (https://github.com/lltcggie/waifu2x-caffe/releases).


 Request environment
----------

Minimum, the following environment is required in order to run this software.

 * OS: (There is no exe for 32bit) Windows Vista or later 64bit
 * Memory: free memory 1GB or more (however, due to the image size to be converted)
 * GPU: (not required if you want to convert in the CPU) Compute Capability 2.0 or more of the NVIDIA GPU
 * That the Visual C ++ 2013 Redistributable package is installed (required)
    - The package is [here] (https://www.microsoft.com/ja-jp/download/details.aspx?id=40784)
    - `After you press the download` button, select the `vcredist_x64.exe`, be sure to download and install.
    - If you can not find, try and search for "Visual C ++ 2013 redistributable package".

If you want to convert in cuDNN further

 * GPU: Compute Capability 3.0 or more of the NVIDIA GPU

If you want to know the Compute Capability of your GPU should be examined in [this page] (https://developer.nvidia.com/cuda-gpus).


 About cuDNN
--------

cuDNN is a library of high-speed machine learning who lodge only in the NVIDIA GPU.
Without using cuDNN can be converted in the CUDA, but there are advantages as follows use cuDNN.

 * Image can be converted more rapidly depending on the type of GPU to be used
 * It is possible to reduce the amount of VRAM (less than half a minimum of CUDA. Difference as the split size increases is gradually open)

It is cuDNN that there is such an advantage, but not be able to distribute the files necessary for the relationship on the operation of the license.
So, people who want to use the cuDNN downloads the [this page] (https://developer.nvidia.com/cuDNN) Windows for binary (v5.1 RC or later) in,
Please put a "cudnn64_5.dll" in the folder of waifu2x-caffe.
In addition, please re-start the software if you put the dll in the middle of running the software.
(To download the cuDNN requires registration and registration to CUDA Registered Developers in the NVIDIA Developer.
 CUDA Registered Developers is probably (simple) does not immediately able to download the cuDNN be registered because ish there is a review. )

The processing speed of the author of the environment, the measurement results of VRAM usage is as follows.

 * GPU: GTX 980 Ti
 * VRAM: 6GB
 * Processing contents: 1000 * 1000 expansion and noise removal in PNG 4ch images, JPEG noise removal level 1, the enlargement ratio 2.00, TTA mode unused
 * Processing time measuring method: measuring the 10 times of the average processing time in the CUI version. However prior to performing the processing twice in the beginning (to not include the time it takes to initialize)
 * VRAM usage calculation method: (maximum was used during the processing in the GUI version of VRAM) - (VRAM usage after you start the GUI version)

cuDNN RGB model

| Split size | processing time | VRAM usage (MB) |
|: ----------- |: ------------- |: ------------------- |
| 100 | 00: 00: 03.170 | 278 |
| 125 | 00: 00: 02.745 | 279 |
| 200 | 00: 00: 02.253 | 365 |
| 250 | 00: 00: 02.147 | 446 |
| 500 | 00: 00: 01.982 | 1110 |

CUDA RGB model

| Split size | processing time | VRAM usage (MB) |
|: ----------- |: ------------- |: ------------------- |
| 100 | 00: 00: 06.192 | 724 |
| 125 | 00: 00: 05.504 | 724 |
| 200 | 00: 00: 04.642 | 1556 |
| 250 | 00: 00: 04.436 | 2345 |
| 500 | unmeasurable | unmeasurable (6144 or more) |

cuDNN UpRGB model

| Split size | processing time | VRAM usage (MB) |
|: ----------- |: ------------- |: ------------------- |
| 100 | 00: 00: 02.831 | 328 |
| 125 | 00: 00: 02.573 | 329 |
| 200 | 00: 00: 02.261 | 461 |
| 250 | 00: 00: 02.150 | 578 |
| 500 | 00: 00: 01.991 | 1554 |

CUDA UpRGB model

| Split size | processing time | VRAM usage (MB) |
|: ----------- |: ------------- |: ------------------- |
| 100 | 00: 00: 03.669 | 788 |
| 125 | 00: 00: 03.382 | 787 |
| 200 | 00: 00: 02.965 | 1596 |
| 250 | 00: 00: 02.852 | 2345 |
| 500 | unmeasurable | unmeasurable (6144 or more) |


 How to use (GUI version)
--------

"Waifu2x-caffe.exe" is a GUI software. Start by double-clicking.
Or when the throw by drag-and-drop files and folders to "waifu2x-caffe.exe" in Windows Explorer, do the conversion in the setting at the time of the last start-up.
In that case, the dialog will be closed automatically after a successful conversion depending on the setting.
In addition, you can make the option settings from the command line, even GUI.
Please read the section of the command-line options (common) and a command line option (GUI version) for more information.

After start-up, and throw in a drag-and-drop an image or a folder to the "input path" column is the "output path" column will be set automatically.
If you want to change the output destination is sure to change the "output path" column.

You can change the conversion settings to your liking.


## Input and output settings
     This setting item group on the input and output files.

### "Input Path"
     It specifies the path of conversion you want to file.
     If you specify a folder, and the file that is attached "extension to be converted in the folder" subfolders within it was also included subject to conversion.
     You can specify more than one file, a folder in the drag.
     If this is the case will be output while maintaining the file, folder structure in the new folder.
    (The input path column "(Multi Files)" is displayed. The output folder name is generated files that were grabbed with the mouse, from the folder name)
     If you press the Browse button to select a file, a single file, or folder, you can select multiple files.

### "Output Path"
     Specify the path where you want to save the image after the conversion.
    If you specify a folder in the "Input Path", it was converted into a specified folder files (the folder structure as it is) and then save. If there is no specified folder will be created automatically.

### "Conversion to the extension in the folder"
     Of the case "input path" is a folder, you specify the image extension of the conversion in the folder.
     The default value is `png: jpg: jpeg: tif: tiff: bmp: is tga`.
     In addition, delimiter is `: is`.
     The search is not case sensitive.
     Example png:. Jpg: jpeg: tif: tiff: bmp: tga

### "Output extension"
     It specifies the format of the converted image.
    Value that can be set to an "output image quality setting," "output depth number of bits" will vary depending on the format that you specify here.

### "Output image quality setting"
     It specifies the image quality of the converted image.
     Can be set value is an integer.
     The scope and meaning of the possible values ??depend on the format that you set in the "Output extension".

      * .jpg: The range of values ??(0 to 100) The higher the number high-quality
      * .webp: The range of values ??(1 to 100) lossless compression that it is the higher the number high-quality 100
      * .tga: The range of values ??(0 to 1) 0 if no compression, RLE compression if 1

### "Number of output depth bit"
     It specifies the number of bits per channel of the post-conversion of the image.
     You can specify a value depends on the format set in the "Output extension".

## Conversion image quality and processing settings
     Processing method of file conversion, is a set group of items related to image quality.

### "Conversion mode"
     Specify the conversion mode.
      * Noise removal and expansion: Performs expansion and noise removal
      * Expansion: Do expansion
      * Noise removal: make noise removal
      * Noise removal and (Auto) expansion: do the expansion. Input will do even if only noise removal of the JPEG image

### "JPEG noise removal level"
    Specify the noise removal level. The higher the level will remove the more powerful noise, but there is also likely to be in the picture that was featureless.

### "Enlarged size,"
    Make the size settings after the enlargement.
      * Specified in the enlargement factor: to enlarge the magnification of the specified image
      * Specified by the width of the converted: while maintaining the aspect ratio of the image, and then expanded to be specified width (in pixels)
      * Specified height of the converted: while maintaining the aspect ratio of the image, and then expanded to become the specified vertical width (in pixels)
    In the case of expansion of more than 2-fold, to expand by 2-fold to more than the specified enlargement ratio (only done the first one if you want to remove the noise), and finally to a reduction in the case of the enlargement factor is not a power multiple of 2 do the processing that. Therefore the result of the conversion might be a picture that was featureless.

###"model"
    It specifies the model to be used.
    Since the optimal model is different by the conversion target of the image, it is recommended that you try out the various models.
      * 2-dimensional illustrations (RGB model): two-dimensional illustrations for the model to convert all RGB image
      * Photos and anime (Photo model): Model for the photos and animation
      * 2-dimensional illustrations (UpRGB model): two-dimensional illustration model to be converted at a high speed and with equal or greater quality than (RGB model). However, since the amount of memory (VRAM) to be consumed than RGB model is large, if you want to kill during the conversion to adjust the partition size
      * Photos and animation (UpPhoto model): photos and animation model to be converted at a high speed and with equal or greater quality than (Photo model). However, since the amount of memory (VRAM) to be consumed than Photo model is large, if you want to kill during the conversion to adjust the partition size
      * 2-dimensional illustrations (Y model): to convert only the luminance of the image two-dimensional illustrations for model

### "Using the TTA mode"
    TTA to specify whether to use (Test-Time Augmentation) mode.
    Instead of conversion and use the TTA mode is 8 times slower, PSNR (one of the evaluation index of the image) is so up about 0.15.

## Processing speed setting
     This setting is a group of items that affect the processing speed of the image conversion.

### "Split size"
    Specifies the width (in pixels) of carrying out the division and the process internally.
    Optimal (processing ends with the fastest) method of determining the numbers are described in the section of "split size".
    Divisor of vertical and horizontal size of the input image is near the top that are delimited by "-------",
    The bottom is a generic division size read from "crop_size_list.txt".
    If the partition size is too large, (If you want to use the GPU amount of VRAM) memory of the amount that is required, please be careful because the software is to kill over a memory that can be used on the PC.
    Because it affects in its own way to processing speed, when a large amount converts the image of the same image size in the folder specified, it is recommended that you convert from by examining the optimal partition size.

## Operation setting
     This setting group that summarizes the operation setting you think that there is no opportunity to change much.

### "Automatic conversion start when setting file input"
     In reference button and drag and drop you to set whether to start the conversion automatically when you specify the input file.
     Set the contents of this item in the case given by the argument of the input file to exe does not affect.
      * It does not start automatically: Do not start the conversion automatically be input the file
      * Start After you enter the file even one: Start to convert the file automatically After you enter even one
      * Start After you enter the folder or multiple files: folder, and then start the conversion automatically Once you enter multiple files. To convert a single image file's only when performing the adjustment of the conversion settings, please at a time when

### "Using Processor"
    Specify the processor to perform the conversion.
      * CUDA (cuDNN if I could use): to perform the conversion using the CUDA (GPU) (If you cuDNN can be used will be used cuDNN)
      * CPU: to perform the conversion using the CPU only

### "I do not want to overwrite the output file"
     If this setting is ON, if there is the same name of the file to write the image does not perform the conversion.

### "With arguments Startup Settings"
     Set the operation in the case given by the argument of the input file to exe.
      * Convert at startup: to start the conversion automatically at startup
      * To end at the time of success: and ends with automatic If you have not failed at the end of conversion

### "Using GPU No"
     You can specify the device number to use if the GPU is a plurality of sheets. If you specify the CPU mode or invalid device number it will be ignored.

### "Input reference at the time fixed folder"
     To secure the folder that is initially displayed when you press the Browse button of the input to the folder that you set here.

### "Output reference at the time fixed folder"
     To secure the output destination folder of the converted image to the folder that you set here.
     In addition, to secure the folder that is initially displayed when you press the Browse button of the output to the folder that you set here.

## Others
     Otherwise, it is the setting item group.

### "UI Languages"
    It sets the UI language.
    The first time you start is chosen the same language as the language setting of your PC. (If it does not exist in English)

### "CuDNN check"
    You can find out whether cuDNN can be used by pressing the "cuDNN check" button.
    If you cuDNN is not available it will be displayed reason.

Conversion and press the "Run" button to begin.
If you want to cancel in the middle and press the "Cancel" button.
However, there is a time lag until the actual stop.
Progress bar shows the progress of when you change a plurality of images.
The remaining estimated time will be displayed in the log, but this is expected when you process multiple files of the same vertical width, width.
So, It does not help if the size of the file is falling apart, do not appear only as "unknown" when image processing is less than or equal to two.


 How to use (CUI version)
--------

"Waifu2x-caffe-cui.exe" is a command-line tool.
`Launch the command prompt`, driving the command, as shown in the following, please use.


The following command output how to use the screen.
`` `
waifu2x-caffe-cui.exe --help
`` `

The following command is an example of the command to execute the image conversion.
`` `
waifu2x-caffe-cui.exe -i mywaifu.png -m noise_scale --scale_ratio 1.6 --noise_level 2
`` `
When you run the above, `mywaifu (noise_scale) (Level2) (x1.600000) .png` the conversion result will be saved.

Command list, please read the section of the command-line options (CUI version) and more information about the command-line options for each command (common).


 Command Line Options (Common)
--------

In this software, you can specify the following options.
In the GUI version if you start with the command line options other than the input file, it does not perform the current options for saving files.
In addition, the options in the GUI version was not specified, use the last time at the end of options.

### - L <string>, --input_extention_list <string>
     input_file is the case of a folder, you specify the image extension of the conversion in the folder.
     The default value is `png: jpg: jpeg: tif: tiff: bmp: is tga`.
     In addition, delimiter is `: is`.
     Example png:. Jpg: jpeg: tif: tiff: bmp: tga

### - E <string>, --output_extention <string>
     input_file is the case of a folder, specify the extension of the output image.
     The default value is `png`.

### - M <noise | scale | noise_scale>, --mode <noise | scale | noise_scale>
     Specify the conversion mode. If you do not specify the `noise_scale` it will be selected.
      * Noise: make the noise removal (more precisely, do the image conversion using a model for noise removal)
      * Scale: do the expansion (to be exact, after being enlarged by the existing algorithm, make the image conversion using a model for the enlarged image supplement)
      * Noise_scale: do the expansion and noise removal (after performing the noise removal, will continue to perform the enlargement process)
      * Auto_scale: do the expansion. Input will do even if only noise removal of the JPEG image

### - S <point with a numerical value>, --scale_ratio <point with number>
     It specifies whether to expand to many times the image. The default value is `2.0`, but you can also specify other than 2.0 times.
     If scale_width or scale_height has been specified, it is priority.
     If you specify a value other than 2.0, perform the following processing.
      * First of all, to cover necessary and sufficient to the specified magnification, Repeat twice expansion.
      * If the number of non-power-of-2 is specified, you can shrink the enlarged image to be specified magnification in a linear filter.

### - W <integer>, --scale_width <integer>
     While maintaining the aspect ratio of the image, and then expanded to be specified width (in pixels).
     It is not possible to specify at the same time as scale_height.

### - H <integer>, --scale_height <integer>
     While maintaining the aspect ratio of the image, and then expanded to become the specified vertical width (in pixels).
     It is not possible to specify at the same time as scale_width.

### - N <0 | 1 | 2 | 3>, --noise_level <0 | 1 | 2 | 3>
     Specify the noise removal level. Since model for noise removal is prepared only Level 0-3,
     Please specify a 0 or 1, 2, or 3.
     The default value is `0`.

### - P <cpu | gpu | cudnn>, --process <cpu | gpu | cudnn>
     Specify the processor to use for processing. The default value is `gpu`.
      * Cpu: to perform the conversion using the CPU.
      * Gpu: to perform the conversion using the CUDA (GPU). Only in the Windows version, you can use the cuDNN if cuDNN can be used.
      * Cudnn: to perform the conversion using the cuDNN.

### - C <integer>, --crop_size <integer>
     You specify the partition size. The default value is `128`.

### - Q <integer>, --output_quality <integer>
     Set the image quality of the converted image. The default value is `-1`
     You can specify a value and meaning varies depending on the format that you set in the "Output extension".
     In the case of -1 is the default value of each image format is used.

### - D <integer>, --output_depth <integer>
     It specifies the number of bits per channel of the post-conversion of the image. The default value is `8`.
     You can specify a value depends on the format set in the "Output extension".

### - B <integer>, --batch_size <integer>
     It specifies the mini-batch size. The default value is `1`.
     mini-batch size is that of the number of simultaneous processing of blocks obtained by dividing the image in the "split size". For example, `If you specify 2`, it will convert every two blocks.
     It will be higher as well GPU utilization and to increase the division size and to increase the mini-batch size, but it is better to increase the partition size that it is felt that the measurement is highly effective.
     (For example, the split size `64`, rather than mini-batch size to` 4`, the partition size `128`, who was mini-batch size to` 1` is completed faster processing)

### --gpu <Integer>
     Specify the GPU device number to use for processing. The default value is `0`.
     GPU device number, please note that starting from zero.
     If you do not want to use the GPU to process it will be ignored.
     Also, if you specify a non-existent GPU device number it will be run with the default GPU.

### - T <0 | 1>, --tta <0 | 1>
     `If ??you specify a 1` use the TTA mode. The default value is `0`.

### -, --ignore_rest
     Ignore all the options after this option is specified.
     It is for the script batch file.


 Command line option (GUI version)
--------

Argument that was not the case in the options specified in the GUI version is recognized as an input file.
The input file is a file, folder, you can specify multiple files and folders at the same time.

### - O <string>, --output_folder <string>
     Set the path to the folder where you want to save the converted image.
     Save the file after conversion into a specified folder.
     The naming convention of the converted file is the same as the output file name, which is determined automatically when you set the input file in the GUI.
     If that has not been specified, it is saved in the same folder as the input file of the first one.

### - Auto_start <0 | 1>
     `Will start automatically convert to be specified at the time of launch the 1`.

### - Auto_exit <0 | 1>
     `If ??you specify a 1`, and ends automatically when conversion if you automatically convert to succeed at startup.

### - No_overwrite <0 | 1>
     `If ??you specify a 1`, if there is the same name of the file to write the image it does not perform the conversion.

### - Y <upconv_7_anime_style_art_rgb | upconv_7_photo | anime_style_art_rgb | photo | anime_style_art_y>, --model_type <upconv_7_anime_style_art_rgb | upconv_7_photo | anime_style_art_rgb | photo | anime_style_art_y>
     It specifies the model to be used.
     Setting items in the GUI as a "model" has been one of the following solutions.
      * Upconv_7_anime_style_art_rgb: 2-dimensional illustrations (UpRGB model)
      * Upconv_7_photo: photos and animation (UpPhoto model)
      * Anime_style_art_rgb: 2-dimensional illustrations (RGB model)
      * Photo: photo and anime (Photo model)
      * Anime_style_art_y: 2-dimensional illustrations (Y model)


 Command line option (CUI version)
--------

### - Version
     Output version information and exit.

### - ?, --help
     It shows how to use, and exit.
     Please, such as when you easily want to see how to use it.

### - I <string>, --input_file <string>
     (Required) The path to the image to be converted.
     If you specify a folder, and then output the image file of the folder or less to all converted specified by output_file by folder.

### - O <string>, --output_file <string>
     The path to the file that you want to save the converted image
     (If input_file is a folder) path to the folder where you want to save the converted image
     (If input_file is an image file) extension (such as last .png) Make sure to enter.
     If you do not specify to determine the file name automatically, and save it in the file.
     The decision rules of the file name,
     `(In the case of noise removal level (noise removal mode)) [original image file name]` `(model name)` `(mode name)` `` `(in the case of a magnification ratio (expansion mode))` `(output (if other than 8-bit) number of bits) ``. output extension `
     Looks like.
     Conserved location is basically will be in the same directory as the input image.

### - Model_dir <string>
     Model specifies the path to the directory that is stored. The default value is `models / upconv_7_anime_style_art_rgb`.
     The standard comes with the following model.
      * `Models / anime_style_art_rgb`: model for the two-dimensional image to convert all RGB
      * `Models / anime_style_art`: model for the two-dimensional image to convert only the luminance
      * `Models / photo`: photo to convert all RGB, model for the animated image
      * `Models / upconv_7_anime_style_art_rgb`: model to be converted at a high speed and with equal or greater quality than anime_style_art_rgb
      * `Models / upconv_7_photo`: model to be converted at a high speed and with equal or greater quality than photo
      * `Models / ukbench`: old-fashioned photographic model (. Only model to expand comes with noise removal is not possible)
     Is basically all right even if you do not specify. Please specify, for example, when you use a non-model and self-made models of default.

### - Crop_w <integer>
     You specify the partition size (width). Value of crop_size will be used if you do not set.
     You may be able to convert a higher speed When you specify a sub-multiple of the width of the input image.

### - Crop_h <integer>
     You specify the partition size (vertical width). Value of crop_size will be used if you do not set.
     There is a vertical conversion can possible if you specify faster the divisor of the width of the image to be input.


 Split size
--------

When waifu2x-caffe (waifu2x it is also) is to convert the image,
They performed one by one conversion by dividing the image into every predetermined size, and finally bound to return to the single image, and the process of.
And the partition size (crop_size) is that of the width of when dividing the image (in pixels).

Not expired use the GPU even during the conversion in CUDA (utilization of the GPU has not gone up nearly 100%) case,
Processing might end early by increasing this number. (To become like can be used up the GPU)
[GPU-Z] (http://www.techpowerup.com/gpuz/) try to adjust while watching the GPU Load (GPU usage rate) and Memory Used (VRAM usage rate), and the like.
In addition, please refer to because there is a characteristic, such as the following.

 * Is not necessarily faster larger the numerical value
 * That's about the number of vertical and horizontal size of the partition size image (or divided by a small number much when), the faster decreasing the amount of waste in the operation. (Seems numerical value that does not fit too much in this condition there is also a case to be the fastest?)
 * If you have a number to a 2-fold, the amount of memory that theoretically use is four times careful not to fall is soft (actually three to four times a place such as) since. Be careful especially since CUDA is consumption of memory is very large compared to the cuDNN


 About alpha channel with image
--------

In this software also supports expansion of the alpha channel with the image.
However, because it has become a process of expanding the alpha channel alone, please be careful because it takes about twice the time as compared to the case there is no expansion of the alpha channel with the image.


 The format of language files
--------

Language files format is JSON.
If you create new language file, add language setting to 'lang / LangList.txt'.
'Lang / LangList.txt' format is TSV (Tab-Separated Values).

  * LangName: Language name
  * LangID: Primary language [See MSDN] (https://msdn.microsoft.com/en-us/library/windows/desktop/dd318693.aspx)
  * SubLangID: Sublanguage [See MSDN] (https://msdn.microsoft.com/en-us/library/windows/desktop/dd318693.aspx)
  * FileName: Language file name

ex.

  * Japanese LangID: 0x11 (LANG_JAPANESE), SubLangID: 0x01 (SUBLANG_JAPANESE_JAPAN)
  * English (US) LangID: 0x09 (LANG_ENGLISH), SubLangID: 0x01 (SUBLANG_ENGLISH_US)
  * English (UK) LangID: 0x09 (LANG_ENGLISH), SubLangID: 0x02 (SUBLANG_ENGLISH_UK)


Refuse
------------

This software is no warranty.
Use under the judgment of the user.
Authors will not assume any obligation.


Acknowledgment
------
Original [waifu2x] (https://github.com/nagadomi/waifu2x), and carried out the production of the model, who have published under the MIT license [ultraist] (https://twitter.com/ultraistter) Mr.,
Based on the original waifu2x [waifu2x-converter] (https://github.com/WL-Amigo/waifu2x-converter-cpp) who have created a [Amigo] (https://twitter.com/WL_Amigo) Mr. (how to write README and LICENSE.txt, I was fairly brought to reference such as how to use the OpenCV)
To, thank you.
In addition, @ paul70078's who have English translation of the message, @yoonhakcher's who have translated into Chinese (Simplified) a message, Chinese @mzhboy who gave me the (Simplified) translation of the pull request,
The message who have translated into Korean @ kenin0726's, @aruhirin's with us to propose the improvement of the Korean translation,
The message who have translated into Chinese (Traditional) @ lizardon1995's, @ yoonhakcher san, thank you to @Scharynche who gave me the pull request of the Turkish translation. 