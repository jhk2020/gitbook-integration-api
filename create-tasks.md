# Create task

*Endpoints are described here require `tasks creation` option enabled for your store, so contact Tipsi if you have errors.*

## Upload image

Use POST request to `/api/rest/v001/store/STORE_ID/image_upload` to upload images for further usage in task creation endpoint.


{% method %}
Upload image to Tipsi server. Use response url to create tasks.

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
Create tasks to process item by Tipsi team.

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
