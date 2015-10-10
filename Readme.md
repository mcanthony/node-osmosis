#Osmosis

HTML/XML parser and web scraper for NodeJS.

##Features

- Fast: uses libxml C bindings
- Lightweight: no dependencies like jQuery, cheerio, or jsdom
- Clean: promise based interface- no more nested callbacks
- Flexible: supports both CSS and XPath selectors
- Predictable: same input, same output, same order
- Detailed logging for every step
- Easy debugging with built-in stack size and memory usage reporting


###Coming soon:

DOM support and the ability to run scripts/CSS without a headless browser.

##Example: scrape all craigslist listings

```javascript
var osmosis = require('osmosis');

osmosis
.get('www.craigslist.org/about/sites') 
.find('h1 + div a')
.set('location')
.follow('@href')
.find('header + div + div li > a')
.set('category')
.follow('@href')
.find('p > a', '.totallink + a.button.next:first')
.follow('@href')
.set({
    'title':        'section > h2',
    'description':  '#postingbody',
    'subcategory':  'div.breadbox > span[4]',
    'date':         'time@datetime',
    'latitude':     '#map@data-latitude',
    'longitude':    '#map@data-longitude',
    'images[]':     'img@src'
})
.data(function(listing) {
    // do something with listing data
})
```

##Install

```
npm install osmosis
```

##Documentation

For documentation and examples check out [https://github.com/rc0x03/node-osmosis/wiki](https://github.com/rc0x03/node-osmosis/wiki)

##Dependencies

- [libxmljs](https://github.com/polotek/libxmljs) - libxml C bindings
- [needle](https://github.com/tomas/needle) - Lightweight HTTP wrapper

##Donate
Donations will accelerate development and improve the quality and stability of this project.

[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?item_name=node-osmosis&cmd=_donations&business=NAXMWBMWKUWUU)
