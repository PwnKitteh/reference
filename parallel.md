---
title: Parallel
date: 2021-7-1 18:28:43
icon: icon-bash
background: bg-gray-400
tags:
    - shell
    - linux
    - parallel
categories:
    - Programming
intro: A quick reference to GNU Parallel commands, which allow you to use multiple cores to complete resource-intensive tasks
---

Getting started {.cols-3}
---------------

### Basic Syntax

```bash
parallel [options] [command [arguments]] < list_of_arguments
parallel [options] [command [arguments]] ( ::: arguments | :::: argfile(s) ) 
```


### Image Conversion

```bash
# Convert all .jpeg files in a directory to .png
find . -name "*jpeg" | parallel -I% --max-args 1 convert % %.png
```

### Audio Conversion

```bash
# Re-encode audio library of .flac files to save disk space
(find -type f -name '*.flac') | parallel opusenc --bitrate 160 {} {.}.opus && mkdir Space_Efficient_Music && mv *.opus Space_Efficient_Music

```

### Un-Zip Archives

```bash
# find and unzip each .zip archive in current directory into its own subfolder
parallel 'mkdir {.}; cd {.}; unzip ../{}' ::: *.zip  
```

### Find and Zip files
```bash
# Find all files matching name*.png and individually gzip them. 
find -type f -name name’*.png’ | parallel gzip –best
```



### Arguments {.row-span-2}

| Expression      | Description                                                           |
| ---             | ---                                                                   |
| `{}`            | Input line, replacement by full line read from input source           |
| `{.}`           | Input line, without extension. Input string with extension removed    |
| `{/}`           | Basename, replacement by input with directory part removed            |
| `::: arguments` | Use arguments from command line as input source instead of stdin      |
| `-P N`          | Number of jobslots on each machine, 0 (default)is as many as possible |

See: [GNU Parallel Reference](https://www.gnu.org/software/parallel/man.html#OPTIONS)



