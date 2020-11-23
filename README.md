# Convolutional Recurrent Neural Network + CTCLoss 

* The images folder contain all the cropped images and preprocessing descriptions
* train.ipynb contains the scripts. Currently its a bit unreadable... will refactor later.

## Run demo

- Use the weights expr/FinalnetCRNN_999_3.pth

- Run demo

  ```sh
  python demo.py -m path/to/model/expr/FinalnetCRNN_249_105.pth -i demo/উত্তরাধিকার_82.jpg
  ```

   ![demo](https://raw.githubusercontent.com/ShadmanRohan/ocr-bengali-crnn/master/demo/%E0%A6%89%E0%A6%A4%E0%A7%8D%E0%A6%A4%E0%A6%B0%E0%A6%BE%E0%A6%A7%E0%A6%BF%E0%A6%95%E0%A6%BE%E0%A6%B0_82.jpg =300*){:height="200px" width="70px"}

  Expected output

  ```sh
  উ-----তত্্্তররাাধিিককাাারর => উত্তরাধিকার
  ```

## Train your data

### Prepare data

#### Folder mode

1. Put your images in a folder and organize your images in the following format:

   `label_number.jpg` 

   For example:

   - English
   ```sh
   hi_0.jpg hello_1.jpg English_2.jpg English_3.jpg E n g l i s h_4.jpg...
   ```
   - Bengali
   ```sh
        উত্তরাধিকার_82.jpg দেশপ্রেমের_70.jpg দেশের_13.jpg ধূলিকণায়_16.jpg বিশাল_6.jpg ...
   ```
   The numbers are used to distinguish the same labels.

2. Run the `create_dataset.py` in `tool` folder by

   ```sh
   python tool/create_dataset.py --out lmdb/data/output/path --folder path/to/folder
   ``` 

3. Use the same step to create train and val data.

4. The advantage of the folder mode is that it's convenient! But due to some illegal character can't be in the path

   So the disadvantage of the folder mode is that it's labels are limited. 



#### File mode

1. Your data file should like

   ```sh
   absolute/path/to/image/উত্তরাধিকার_82.jpg
        উত্তরাধিকার_82
   absolute/path/to/image/দেশপ্রেমের_70.jpg
        দেশপ্রেমের_70
   absolute/path/to/image/দেশের_13.jpg
        দেশের_13
   absolute/path/to/image/ধূলিকণায়_16.jpg
        ধূলিকণায়
   absolute/path/to/image/বিশাল_6.jpg
        বিশাল_6
   absolute/path/to/image/xxx.jpg
   label of xxx.jpg
   .
   .
   .
   ```

   > DO REMEMBER:
   >
   > 1. It must be the absolute path to image.
   > 2. The first line can't be empty.
   > 3. There are no blank line between two data.



2. Run the `create_dataset.py` in `tool` folder by

   ```sh
   python tool/create_dataset.py --out lmdb/data/output/path --file path/to/file
   ```

   

3. Use the same step to create train and val data.



### Change parameters and alphabets

Parameters and alphabets can't always be the same in different situation. 

- Change parameters

  Your can see the `params.py` in detail.

- Change alphabets

  Please put all the alphabets appeared in your labels to `alphabets.py` , or the program will throw error during training process.



### Train

Run `train.py` by

```sh
python train.py --trainroot path/to/train/dataset --valroot path/to/val/dataset
```

## Dependence

- Python3.6.5
- torch==1.2.0
- torchvision==0.4.0


## Reference

[meijieru/crnn.pytorch](<https://github.com/meijieru/crnn.pytorch>)

[Sierkinhane/crnn_chinese_characters_rec](<https://github.com/Sierkinhane/crnn_chinese_characters_rec>)

