---
layout: post
comments: true
title: Cool Convoluted Commands
---

Just a collection of useful commands that I find cool/interesting.
&nbsp;


You will require **coreutils** to run the MacOS commmands. (`brew install coreutils`) 
&nbsp;

[Don't have homebrew? Please install it.](https://brew.sh/)
&nbsp;
&nbsp;
&nbsp;


<details><summary><b>Copy N random files from one directory to another</b></summary>

<ul style="font-size:16px">

<p> Good for messing around with a small sample from a large dataset. You can also add a regex pattern if you wish to filter.</p>

<p> MacOS: </p>
<code>
```
gshuf -zn <FILE_COUNT> -e <PATTERN> | xargs -0 gcp -vt <TARGET_DIR>
```
</code>

<p>Linux:</p>
<code>
```
shuf -zn <FILE_COUNT> -e <PATTERN> | xargs -0 cp -vt <TARGET_DIR>
```
</code>

<p>You may encounter an error: <code>`shuf: Argument list too long`. </code> </p>

<p> In this case, we can pipe the arguments as follows: </p>

<p>MacOS:</p>
<code>
find <SOURCE_DIR> -mindepth 1 -maxdepth 1 ! -name '<PATTERN>' -print0 | gshuf -n <FILE_COUNT> -z | xargs -0 gcp -t <TARGET_DIR>
</code>

<p>Linux:</p>
<code>
find <SOURCE_DIR> -mindepth 1 -maxdepth 1 ! -name '<PATTERN>' -print0 | shuf -n <FILE_COUNT> -z | xargs -0  cp -t <TARGET_DIR>
</code>

<p>You can even tweak these commands so that you can copy N random **lines** from one file to another . Useful in those cases where all your data is in one file. (*Hint:* use 🐱)</p>


</details>


<details><summary>Find non-empty files in a directory</summary>
<p>

Same for MacOS and Linux 
```
find <DIR_NAME> -not -empty -ls 
```
You can change this command to find the names of the empty file names. 
```
find <DIR_NAME> -empty -ls
```

And to find the number of files, simply pipe the output of any of these commands to `wc - l`.

</p>
</details>

<details><summary>Join files horizontally using a Primary Key</summary>
<p>
Same for MacOS and Linux 

Useful for joining CSV's. This process requires that your data is complete and clean, so not sure how useful this is. However, it's a very fast procedure to join two CSVs after removing missing information (I will add a few commands that can help with this!). 

Suppose you have the following two CSV's: 
```
> cat 1.csv
Arjun,Purple,MacOS,Table Tennis
Sanja,Black,Ubuntu,Netflix
Russell,Red,Windows,Dota2


> cat 2.csv
Russell,C++
Sanja,Pyhon
Arjun,PHP
```
And we want to create a single CSV using the names as our primary key.

We could do the following:

Sort both files by their primary key (located in the first column).
```
sort -t"," -k1  1.csv > 1_sorted.csv
sort -t"," -k1  2.csv > 2_sorted.csv
``` 
Now cut the 2nd column from `2_sorted` and add to `1_sorted` using the `cut` and `paste` commands.
```
cut -d',' -f2 2_sorted.csv > 2_sorted_fav_lang.csv
paste -d, 1_sorted.csv 2_sorted_fav_lang.csv > final.csv
```
Let's take a look:
```
> cat final.csv
Arjun,Purple,MacOS,Table Tennis,PHP
Russell,Red,Windows,Dota2,C++
Sanja,Black,Ubuntu,Netflix,Pyhon
```
</p>
</details>
&nbsp;
&nbsp;
&nbsp;

#### More to come!
&nbsp;
&nbsp;
&nbsp;
&nbsp;








