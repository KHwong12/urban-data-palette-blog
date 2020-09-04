This document is used as notes to understand the structure of the theme

### header image

Absolute directory the hugo looking for finding header image is `static/images`, while the cover photo will be in `static/post/POST-FOLDER/COVER.jpg`
To avoid manual edits of the theme, Image tag for yaml will be

```
image: "../post/POST-FOLDER/COVER.jpg"
```
