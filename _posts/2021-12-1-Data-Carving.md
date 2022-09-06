---
layout: post
title: "File Recovery"
date: 2021-12-1
image: ../../assets/img/Posts/file recovery.jpg
categories: [DFIR]
tags: [data carving, file recovery]
---

# File Recovery and Data Carving with Foremost, Scalpel, and Bulk Extractor

## Foremost

Foremost is a forensic program to recover lost or deleted files using a technique called `data carving`,based on their headers, footers, and internal data structures .

Foremost can work on image files, such as those generated by dd, Safeback, Encase, etc, or directly on a drive. The headers and footers can be specified by a configuration file or you can use command line switches to specify built-in file types. These built-in types look at the data structures of a given file format allowing for a more reliable and faster recovery.

### **How to install**

`sudo apt install foremost`

It can also be found in Kali linux under **Applications > Forensics > foremost**

### Usage

```
foremost -v -t all -i Evidence.dd -o /home/sansforensics/Desktop/Case1/Foremost
```

`-v` has been used to give us verbose output.

`-i` has been used to specify the image file

`-t all` has been used to specify that we want to extract all possible file types

![image](https://user-images.githubusercontent.com/58165365/141350640-25d2b76d-2876-4d96-9bcf-0ea695438dae.png)

You can also specify specific file formats that you want to carve as shown below.

```
foremost -v -t jpg,png,gif -i EvidenceDD -o /home/sansforensics/Desktop/Case1/Foremost
```

## scalpel

scalpel is a fast file carver that reads a database of header and footer definitions and extracts matching files from a set of image files or raw device files.

scalpel is filesystem-independent and will carve files from FAT16, FAT32, exFAT, NTFS, Ext2, Ext3, Ext4, JFS, XFS, ReiserFS, raw partitions, etc.

scalpel is a complete rewrite of the Foremost 0.69 file carver and is useful for both digital forensics investigations and file recovery.Scalpel aims to address the high CPU and RAM usage issues of Foremost when carving data.

### **How to install**

`sudo apt install scalpel`

### Usage

If you run foremost for the first time, you will encounter the following error

![image](https://user-images.githubusercontent.com/58165365/141351207-be63fbd3-0540-4bf6-af1c-64f891447c5f.png)

The error itself is preety informative. Unlike Foremost, file types of interest must be specified by the investigator in the Scalpel configuration file. `/etc/scalpel/scalpel.conf`

By default, the file types have been commented out (#) as shown below.

![image](https://user-images.githubusercontent.com/58165365/141351363-f6e207dc-e4f8-44e7-84ae-9406d6789736.png)

In this example, I want to search for deleted Image files, so I uncomment the following lines: **(gif,jpg,png)**

![image](https://user-images.githubusercontent.com/58165365/141351574-198be46e-2ac9-4ffc-8d90-60a693b57fd0.png)

If we run the command again this time, it should be able to carve out for us the files specified.

![image](https://user-images.githubusercontent.com/58165365/141351688-faa50f6e-2073-4d11-9e31-06689f580da9.png)

Although Scalpel returned more files than Foremost,some are false positives or duplicates. Carry out your own exercise in comparing the carved files found by both Foremost and Scalpel and see which tool would be best for you.😉

I'll leave a link where you can download an evidence file and compare outputs by the different tools.

[11-carve-fat.dd](http://dftt.sourceforge.net/test11/index.html)

## bulk-extractor

Foremost and Scalpel, as we've seen so far, are quite impressive at file recovery and carving, but are limited to specific file types. For further extraction of data, we can use Bulk Extractor.While Foremost and Scalpel can recover images, audio, video, and compressed files, Bulk Extractor extracts several additional types of information that can be very useful in investigations.

Although Bulk Extractor is quite capable of recovering and carving image, video, and document type files, other data that can be carved and extracted by Bulk Extractor includes:

- Credit card numbers
- Email addresses
- URLs
- Online searches
- Website information
- Social media profiles and information.

_Source: Digital Forensics with Kali Linux - Shiva V.N. Parasram_

### **How to install:**

`sudo apt install bulk-extractor`

### Usage

You can use this ([terry-workusb-2009-12-11.E01](https://downloads.digitalcorpora.org/corpora/scenarios/2009-m57-patents/drives-redacted)) evidence file for practice with bulk-extractor.

Like Foremost and Scalpel, the syntax for using bulk_extractor is quite simple and requires that an output folder (`-o`) and the forensic image be specified.

`bulk_extractor terry-work-usb-2009-12-11.E01 -o bulk_output`