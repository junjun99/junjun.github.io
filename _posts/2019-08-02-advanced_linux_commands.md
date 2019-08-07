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
<style>
         pre {
            overflow-x: auto;
            white-space: pre-wrap;
            white-space: -moz-pre-wrap;
            white-space: -pre-wrap;
            white-space: -o-pre-wrap;
            word-wrap: break-word;
         }
</style>


<details><summary><b>Copy N random files from one directory to another</b></summary>

<p> Good for messing around with a small sample from a large dataset. You can also add a regex pattern if you wish to filter.</p>

<p> MacOS:<br>
<pre>
gshuf -zn <i>FILE_COUNT</i> -e <i>PATTERN</i> | xargs -0 gcp -vt <i>TARGET_DIR</i>
</pre>
</p>

<p>Linux:<br>
<pre>
shuf -zn <i>FILE_COUNT</i> -e <i>PATTERN</i> | xargs -0 cp -vt <i>TARGET_DIR</i>
</pre>
</p>

<p>You may encounter an error: <code>shuf: Argument list too long</code> <br>
In this case, we can pipe the arguments as follows: </p>

<p>MacOS:<br>
<pre>
find <i>SOURCE_DIR</i> -mindepth 1 -maxdepth 1 ! -name <i>PATTERN</i> -print0 | gshuf -n <i>FILE_COUNT</i> -z | xargs -0 gcp -t <i>TARGET_DIR</i>
</pre>
</p>

<p>Linux:<br>
<pre>
find <i>SOURCE_DIR</i> -mindepth 1 -maxdepth 1 ! -name <i>PATTERN</i> -print0 | shuf -n <i>FILE_COUNT</i> -z | xargs -0  cp -t <i>TARGET_DIR</i>
</pre>
</p>

<p>You can even tweak these commands so that you can copy N random <b>lines</b> from one file to another . Useful in those cases where all your data is in one file. (<b>Hint:</b> use 🐱)</p>


</details>


<details><summary><b>Find non-empty files in a directory</b></summary>
<p>

Same for MacOS and Linux <br>
<pre>
find <i>DIR_NAME</i> -not -empty -ls 
</pre>
</p>
<p>
You can change this command to find the names of the empty file names. <br>
<pre>
find <i>DIR_NAME</i> -empty -ls
</pre>
</p>
<p>
And to find the number of files, simply pipe the output of any of these commands to <code>wc - l</code>
</p>
</details>



<details><summary><b>Join files horizontally using a Primary Key</b></summary>
<p>
Same for MacOS and Linux <br>
</p>
<p>
Useful for joining CSV's. This process requires that your data is complete and clean, so not sure how useful this is. However, it's a very fast procedure to join two CSVs after removing missing information (I will add a few commands that can help with this!). 
</p>
<p>
Suppose you have the following two CSV's: <br>
<pre>
% cat 1.csv
Arjun,Purple,MacOS,Table Tennis
Sanja,Black,Ubuntu,Netflix
Russell,Red,Windows,Dota2

% cat 2.csv
Russell,C++
Sanja,Pyhon
Arjun,PHP
</pre>
<br>
And we want to create a single CSV using the names as our primary key.<br>

We could do the following:<br>

Sort both files by their primary key (located in the first column).<br>
<pre>
sort -t"," -k1  1.csv > 1_sorted.csv
sort -t"," -k1  2.csv > 2_sorted.csv
</pre><
Now cut the 2nd column from <code>2_sorted</code> and add to <code>1_sorted</code> using the <code>cut</code> and <code>paste</code> commands.<br>
<pre>
cut -d',' -f2 2_sorted.csv > 2_sorted_fav_lang.csv
paste -d, 1_sorted.csv 2_sorted_fav_lang.csv > final.csv
</pre>
Let's take a look:<br>
<pre>
> cat final.csv
Arjun,Purple,MacOS,Table Tennis,PHP
Russell,Red,Windows,Dota2,C++
Sanja,Black,Ubuntu,Netflix,Pyhon
</pre>
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








