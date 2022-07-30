---
title: Quick start, Azure blob storage
author: Youngjin Kwak
date: 2022-07-30 13:35:00 +0800
categories: [Azure, storage]
tags: [azure, storage]
---
![azure](../images/azure.jpg)

In this quickstart, you create blob storage <br>
[Microsoft official document](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)


# Getting started
## Step 1
Navigate to the azure portal, [link](https://portal.azure.com). <br>
If you don't have account yet, register azure first!

## Step 2
![image](../images/azure-database/one.png)
- Click the "+ create resource" on the tab

## Step 3
![image](../images/azure-blob-storage/1.png)
- Select "Storage account" or "create" under it

## Step 4
![image](../images/azure-blob-storage/2.png)
- Select proper subscription
- Create new resource group or select group that you already have
- Type storage account name. This field can contain only lowercase letters and numbers and must be between 3 and 24 characters.
- Select your Region
- If you would like to low price of blob storage, go to step 5.
- Press button "Review + create"

## Step 5
This step is talking about low price of blob. If you don't need it goes to next step
![image](../images/azure-blob-storage/3.png)
![image](../images/azure-blob-storage/4.png)
- In Redundancy, "select locally-redundant storage (LRS") option
- Go to advanced tab
- Change access tier to Cool

## Step 6
![image](../images/azure-blob-storage/5.png)
- Check your output

# How to get access keys
![image](../images/azure-blob-storage/6.png)
- In the left drawer, find security + networking
- Click "access keys" menu

# Conclusion
In container menu, you can see the files that you upload

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
