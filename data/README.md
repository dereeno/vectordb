# Addgene DnaMolecules

Addgene's collection of public DnaMolecules is obtained by downloading
a nightly JSON dump of all plasmids in their database. The format of this
blob is:

```JSON

{"plasmids":  [{plasmid1, plasmid2, ..., plasmid 39401}]}

```

This is very large and can not be pushed to github as a single file nor
managed efficiently with git.

Therefore the nightly download is reformatted using ```jq``` and
```split```.

This can be done in one line with 

```sh
jq -c '.plasmids|sort_by(.id)|.[]' < addgene-plasmids-sequences.json | split -d --additional-suffix='.json' - 'addgene-plasmids-'
```


The first command is 
```jq -c '.plasmids|sort_by(.id)|.[]?' < addgene-plasmids-sequences.json```
which reads the json file, unwrapps the array of records, sorts them by
their id, filters any null records, and prints them to stdout with one
json record on each line.

The second command is ```split -d --additional-suffix='.json' - 'addgene-plasmids-'```
which splits the line-oriented json stream from the first command into
1000 line buckets. Because the first command sorts the stream, there
should be a 1 to 1 corespondance between changed lines and changed
records, and these changes should be localized to only a single bucket.
This will enable diff, git, and other line oriented unix tools to work
with these records efficiently.

These two commands can be piped together. You will also need to use
```zmv 'addgene-plasmids-[0-9][0-9]' '$f.json'``` to add the json suffix
to the resulting buckets.

*Note: split should also be able to add this suffix and jq can be
configured to reformat the separator in the json documents to use a more
portable ```---``` instead of a new line.*

