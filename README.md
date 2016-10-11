# 4d-component-generate-icon
Generate 4 state icons using SVG filters

```
$image:=Four_state_icon ($image)
```

###Example

```
$folderPath:=Get 4D folder(Current resources folder)+"src"+Folder separator
DOCUMENT LIST($folderPath;$filePaths;Ignore invisible | Absolute path)

$folderPath:=Get 4D folder(Current resources folder)+"dst"+Folder separator
CREATE FOLDER($folderPath;*)

For ($i;1;Size of array($filePaths))
  $filePath:=$filePaths{$i}
  If (Is picture file($filePath))
    READ PICTURE FILE($filePath;$image)
    $filePath:=$folderPath+Get picture file name($image)
    $image:=Four_state_icon ($image)
    WRITE PICTURE FILE($filePath;$image)
  End if 
End for 

SHOW ON DISK($folderPath)
```

###Source code

SVG filters are used internally.

```
C_PICTURE($1;$0)

  // Original image
$normal:=$1

$svg:=SVG_New 
$g:=SVG_New_group ($svg)
$image:=SVG_New_embedded_image ($g;$normal)

  //Click: add more bright
SVG_SET_BRIGHTNESS ($g;1.2)
$click:=SVG_Export_to_picture ($svg)

  //Hover: add more bright to previous image
SVG_SET_BRIGHTNESS ($g;1.35)
$hover:=SVG_Export_to_picture ($svg)

  //Disabled: reduce brightness and set grayscale
SVG_SET_BRIGHTNESS ($g;0.7)
$disabled:=SVG_Export_to_picture ($svg)
TRANSFORM PICTURE($disabled;Fade to grey scale)

SVG_CLEAR ($svg)

$0:=$normal/$click/$hover/$disabled
```
