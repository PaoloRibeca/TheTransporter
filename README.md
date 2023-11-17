# The Transporter

The Transporter is a small suite of utility programs to transfer a set of annotated features from one genome to a (possibly not that) closely related one. It was initially written as a re-implementation of a tool in the spirit of GATU and others, but it evenutally morphed into something a bit different. Typical use cases are viral or bacterial genomes, although there is no real reason why things shouldn't scale up to larger genomes &mdash; but beware, we never really tested the method on those, so you are on your own if you want to go there... 

> The Transporter is currently unpublished. **You are welcome to use it, but you must not redistribute it**.

Bug reports are always appreciated. Please send them to [paolo.ribeca@gmail.com](mailto:paolo.ribeca@gmail.com). Thank you.

## Dependencies

The Transporter depends on:
* Standard UNIX toolchain utilities (`bash`, `AWK`, etc.)
* A few programs from [BiOCamLib](https://github.com/PaoloRibeca/BiOCamLib). Installation instructions can be found there, but the process is usually very simple and you can just copy pre-compiled binaries across
* Program `transeq` from the EMBOSS suite. EMBOSS can be installed through `conda` or compiled from scratch after downloading it from [here](https://emboss.sourceforge.net/download/). Compilation is straightforward (`./configure` and `make`)
* Depending on the annotation method you'd like to use, external programs such as BLAST, Splign, ...
Unfortunately, Splign is notoriously difficult to compile. In order to simplify installation, static binaries pre-compiled for Linux and independent of the kernel version are provided in directory [`Dependencies`](Dependencies) for Splign and all other dependencies.

## Examples of use

We use the files in the directory Test as examples.

The basic command specifies as input an annotation and a FASTA file to be annotated:

```bash
$ TheTransporter -t Test/ASFV_de_novo.fasta -a Test/ASFV_Cameroon_2016.gbk -o Test
```
This will generate an output `Test.gb` in GenBank format (which is the default).

