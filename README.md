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
