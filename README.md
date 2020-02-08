## Vuepress-sidebar-generator

### What's this for ? 

You needn't modify your `.vuepress/config.js` after you add a new markdown file to your directory



### How to Use ?

Your directory structure may like this

``` 
├── .vuepress
├── README.md
├── foo
│   ├── README.md
│   └── one.md
└── bar
    └── README.md

```

Copy this code to your `.vuepress/config.js`

``` javascript
const fs = require('fs')
function getSidebar(dir) {
    const files = fs.readdirSync(`${__dirname}/../${dir}`)
    const sidebar = files.map(file => {
        let fileName = file.split('.')[0]
        if (fileName.toUpperCase() === 'README') {
            return ''
        }
        else {
            return fileName
        }
    })
    return sidebar
}

module.exports = {
    themeConfig: {
        sidebar: {
            '/foo/': [
                ...getSidebar('foo')
            ],
            'bar': [
                 ...getSidebar('bar')
            ],
            // Or you can use this
            '/foo/': getSidebar('foo'),
            '/bar/': getSidebar('bar') 
        }
    }
}
```



