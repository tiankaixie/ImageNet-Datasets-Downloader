# ImageNet Downloader

This is ImageNet dataset downloader. **You can create new datasets from subsets of ImageNet by specifying how many 
classes you need and how many images per class you need.** 
This is achieved by using image urls provided by ImageNet API.


[In this blog post](https://towardsdatascience.com/how-to-scrape-the-imagenet-f309e02de1f4) I wrote in a bit more detail how and why I wrote the tool. Also, I did a little analysis of the current state of the ImageNet URLs in the post. 

This software is written in Python 3

## Usage


The following command will randomly select 100 of ImageNet classes with at least 200 images in them and start downloading:
```
python ./downloader.py \
    -data_root /data_root_folder/imagenet \
    -number_of_classes 100 \
    -images_per_class 200
```


The following command will download 500 images from each of selected class:
```
python ./downloader.py 
    -data_root ../ -use_class_list True -class_list n02691156 n04524313 n01503061 n02121620 n02430045 n02084071 n01639765 n02374451 n04194289 n04490091 -images_per_class 500 
```
You can find class list in [this csv](https://github.com/mf1024/ImageNet-datasets-downloader/blob/master/classes_in_imagenet.csv) where I list every class that appear in the ImageNet with number of total urls and total flickr urls it that class.

# Multiprocessing workers 

I've implementet parallel request processing and I've added **multiprocessing_workers parameter** which by default is 8. You can turn it higher, but I havent yet tested the limits of flickr allowed bandwith myself, so use it with care and you will have to find the limits yourself if you want to go for the maximum speed.

You can do something like this:

```
python ./downloader.py \
    -data_root /data_root_folder/imagenet \
    -number_of_classes 1000 \
    -images_per_class 500 \
    -multiprocessing_workers 24
```
