# The Transporter

The Transporter is a small suite of utility programs to transfer a set of annotated features from one genome to a (possibly not that) closely related one. It was initially written as a re-implementation of a tool in the spirit of GATU and others, but it evenutally morphed into something a bit different. Typical use cases are viral or bacterial genomes, although there is no real reason why things shouldn't scale up to larger genomes &mdash; but beware, we never really tested the method on those, so you are on your own if you want to go there... 

A manuscript explaining the techniques we use is in preparation.

Bug reports are always appreciated. Please send them to [paolo.ribeca@gmail.com](mailto:paolo.ribeca@gmail.com). Thank you.

## Dependencies

The Transporter depends on:
* Standard UNIX toolchain utilities (`bash`, `AWK`, etc.)
* A few programs from [BiOCamLib](https://github.com/PaoloRibeca/BiOCamLib). Installation instructions can be found there, but the process is usually very simple and you can just copy pre-compiled binaries across. Alternatively, the `BiOCamLib` binaries are provided in directory [`Dependencies`](Dependencies)
* Depending on the annotation method you'd like to use, external programs such as BLAST, Splign, ...

Unfortunately, Splign is notoriously difficult to compile. In order to simplify installation, static binaries pre-compiled for Linux and independent of the kernel version are provided in directory [`Dependencies`](Dependencies) for Splign and all other dependencies. Just copy them to some place in your PATH, and ideally you won't need to install anything else.

## Examples of use

We use the files in the directory Test as examples.

The basic command specifies as input an annotation and a FASTA file to be annotated:

```bash
$ TheTransporter -t Test/ASFV_de_novo.fasta -a Test/ASFV_Cameroon_2016.gbk -o Test
```
This will generate an output `Test.gb` in GenBank format (which is the default).

## Methods

Each feature appearing in the output annotation file will contain a note summarising how it was generated, for instance
```
transported from KJ705001:-:8687-9763+9874-10092 (method=protein->DNA, similarity=0.72)
```
A quick correspondence table between the method name and the program actually used to generate the feature is as follows:
Method name in the feature | Program
---------------------------|--------
RNA->DNA                   | `splign`
protein->DNA               | `tblastn`
protein->ORF               | `blastp`
ORF                        | `transeq`
