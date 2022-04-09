---
title: Console
date: 2018-09-15T07:42:34.000+00:00
slug: console

---
## Changing logo

blank,``code``

## Adding icons

blank,

```javascript
import { MoonIcon, SunIcon } from 'vue-feather-icons'

export default {
  components: {
    MoonIcon,
    SunIcon
  },
...
```

And then the icon can be used like this:

```html
<sun-icon class="sun" />
```

## Changing colors

blank,

```scss
// Dark theme
$backgroundDark: #18191a;
$sidebarDark: #2a2c2f;
$textDark: #fff;

// Bright theme
$backgroundBright: #fff;
$sidebarBright: #f3f4f5;
$textBright: #2a2c2f;

// Brand
$brandPrimary: #10c186;
```

## Changing font

dddd

```bash
yarn add typeface-open-sans
```

Then, on line 7 in `src/main.js` you change the line to:

```javascript
require('typeface-open-sans')
```

ok

```scss
font-family: 'Open Sans', sans-serif;
```

You're done!

## Edit the sidebar

Thiss:

```json
{
  "section": "Introduction",
  "topics": [
    {
      "title": "Getting started",
      "slug": "getting-started"
    }
  ]
}
```

End