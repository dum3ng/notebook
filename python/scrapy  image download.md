Scrapy use `Item` and `Pipeline` to do extra process after get the response. 

Every item can be processed by a sequence of pipelines, and there are built-in pipelines for media downloading in scrapy. The hirachy is:

```flow
one=>start: MediaPipeline
two=>start: FilesPipeline
three=>start: ImagesPipeline

one->two->three

```

## default image download process
### add settings

In the `settings.py`, add:

```python
ITEM_PIPELINES = {
  'scrapy.pipelines.images.ImagesPipeline': 1
  }
  
IMAGE_STORE = '/Users/me/Pictures'
```

### return infomation
Then in a spider's `parse` function:

```python
def parse(self, response):
  return image_urls = response.xpath('//img')
```

The results returned by spiders will go through the item pipelines you just enabled. Since the imagePipeline will work when the item contains a key named 'iamge_urls'( by default) or a spider returned a variable with the same name, the imaged will be stored in the location you configured in the `settings.py`.

## customize image download
The default image file name is a sha1 hash of the image url and a `full` prefix. To customize the file name, we need to make a subclass of `ImagesPipeline`:

```python
class MyImagesPipeline(ImagesPipeline):
  def file_path(self, request, response=None, info=None):
    image_guid = request.url.split('/')[-1] or request.url
    return image_guid
```

and change the `settings.py`:

```python
ITEMS_PIPELINE = {
  'project.pipelines.MyImagesPipeline': 1
  }
```

This will just use the name in the url to image.

### add extra infomation
Sometime we want to add extra infomation to a request, say we want to save images to a specified subfolder.

**1, add an item**

```python
## in items.py
class MyImagesItem(Object):
  image_urls = scrapy.Field()
  images = scrapy.Field()
  folder = scrapy.Field()
```

**2, override the `get_media_request`**

```python
class MyImagesPipeline(ImagePipeline):
  #.... 
  def get_media_requests(self, item, info):
    return [scrapy.Request(x, meta={'folder': item['folder']}) for x in item.get('image_urls', [])]
```

**3, add info in spider**

```python
from project.items import MyImagesItem

class ImageSpider(scrapy.Spider):
  #...
  def parse(self, response):
    urls = response.xpath('//img//@src').extract()
    title = response.xpath('//h1[class="title"]/text()').extract()
    return MyImagesItem(image_urls=urls, folder=title)
```

**Done!**
Now the images will be saved under the folder with name of the page title.

