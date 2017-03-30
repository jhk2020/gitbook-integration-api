# Label Processing Tasks Guide

*Note: to create tasks via integration API you should have this option enabled by Tipsi team. Please contact support if API doesn't work for you*

Label processing tasks is a way to match products manually by Tipsi team. It requires product front label picture and optionally back label, for wines it's also recommended to send vintage. If vintage is not send and there is no vintage on wine label, the most recent vintage will be used by default.

Label processing tasks are created in 3 steps:

1. Create inventory item [API reference](/endpoints.md#create-wine-inventory)
2. Upload image (or images)
3. Create label tasks

## Upload image

Perform POST request to `/api/rest/v001/store/STORE_ID/image_upload` to upload image. The returned image URL will be used in `create tasks` API.


{% method %}
Upload image to Tipsi server. The endpoint will return image URL, which can be used later for label tasks creation.

{% sample lang="postman" %}
![](/assets/image_upload.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/image_upload'
with open('image.png', 'rb') as file_obj:
    params = {'image': file_obj}
    result = session.post(url, files=params).json()
```
{% endmethod %}


## Create task for unmatched inventory item

You can create task by sending POST to `/api/rest/v001/store/STORE_ID/wine/INVENTORY_ID/create_task` or `/api/rest/v001/store/STORE_ID/drink/INVENTORY_ID/create_task`.

{% method %}
Create product label processing tasks, those tasks will be processed by Tipsi team.

{% sample lang="postman" %}
![](/assets/create_task.png)

{% sample lang="python" %}
```python
url = 'https://integration-test.gettipsi.com/api/rest/v001/store/STORE_ID/wine/INVENTORY_ID/create_task'
data = {'front_image': front_image_url,
        'back_image': back_image_url,
        'vintage': '2015'}
result = session.post(url, data=data).json()
```
{% endmethod %}
