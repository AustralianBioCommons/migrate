Migrate
================

## [Description](https://peterbeerli.com/migrate-html5/about.html)

| Repository / Registry |                          Available?                           |
| --------------------- | :-----------------------------------------------------------: |
| GitHub                |                                                               |
| bio.tools             |                [●](https://bio.tools/MIGRATE)                 |
| BioContainers         |       [●](https://biocontainers.pro/#/tools/migrate-n)        |
| bioconda              | [●](https://bioconda.github.io/recipes/migrate-n/README.html) |

## Required (minimum) inputs / parameters

As an example, we show how to run the sequencing data for a few thousand
target loci from a few populations in phylip format.

This requires at least three files:

1.  migrate\_input\_interleaved.phy
    
      - Sequencing data of tested samples in phylip multiple sequence
        alignment format. This is the actual data file.

2.  parmfile
    
      - Text file with model specification. This file has numerical
        parameters for the various simulation steps. The parameter file
        is quite long: please refer to [official migrate tutorial
        examples](http://peterbeerli.com/workshops/mbl/2016/tutorial)
        from the developer.
      - There are more details about parameters in the
        [documentation](https://peterbeerli.com/programs/migrate/distribution_4.x/migratedoc4.x.pdf)
      - **Note:** Output file names for the PDF and other outputs should
        start without tilde or slash referencing

<!-- end list -->

``` …
outfile=projectfolder/test_migrate_run1
…
pdf-outfile=projectfolder/test_migrate_run1.pdf
```

3.  migrate\_job
    
      - Gadi PBS job card: the text file with user allocation details
        and resources required for the job.

<!-- end list -->

``` #!/bin/bash
#PBS -q normal
#PBS -P xyz0000
#PBS -l walltime=48:00:00,ncpus=48,mem=190GB
#PBS -l storage=scratch/xyz0000
module load openmpi/4.0.2
mpirun ~/migrate-n -nomenu ~/projectfolder/parmfile
```

Where:

`#PBS -q normal`

Queue system to choose there are other queues: express, hugemem,
gpuvolta, copyq. Check opus documentation for details.

`#PBS -P xyz0000`

This uses the project ID from the Mancini site. You have to be assigned
to this project by its administrator.

`#PBS -I walltime=48:00:00,ncpus=48,mem=190GB`

A wall time of 48hrs is the maximum for jobs using up to 672 CPUs. The
memory unit of 190GB is linked to a 48 CPU block. Check your limits on
this [page](https://opus.nci.org.au/display/Help/Gadi+Queue+Limits).

`module load openmpi/4.0.2`

This is the first command. It allows preloading of the libraries
required for multithreaded migrate:

`mpirun ~/migrate-n -nomenu ~/projectfolder/parmfile`

Executing second command with migrate binaries taken directly from home
folder and parameter file from subdirectory named
projectfolder/parmfile. The flag `-nomenu` allows you to run migrate
without an interactive menu (all info is in parmfile).

## Key link(s) & additional information (e.g. input(s), parameter(s), output(s))

## Third party tools / dependencies

# Diagram

Not available.

# Usage

## Summary

<font size="-1.5">

| Version | Infrastructure                   | Scheduler | Workflow manager | Container | Install method |
| ------- | -------------------------------- | --------- | ---------------- | --------- | -------------- |
| 4.4.4   | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | PBSpro    | None             | None      | Module         |

</font>

## High level resource usage

<font size="-1.5">

| Version | Group | Model            | Number of loci | Number of samples | Replicates? | Hours required              | Cores | Peak RAM in GB (requested) | Drive (GB) | HPC-HTC                                         | Month-Year |
| ------- | ----- | ---------------- | -------------- | ----------------- | ----------- | --------------------------- | ----- | -------------------------- | ---------- | ----------------------------------------------- | ---------- |
| 4.4.4   | OMG   | SAMI\_1617\_run3 |                | 60                | 1           | 5:38:29                     | 96    | 205.89 (380)               | 0.00816    | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |
| 4.4.4   | OMG   | SAMI\_1617\_run4 | 1616           | 60                | 1           | 34:56:51                    | 96    | 220.7 (380)                | 0.00816    | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |
| 4.4.4   | OMG   | SAMI\_1617\_run5 | 1616           | 60                | 1           | 31:37:19                    | 96    | 220.97 (380.0)             | 0.00816    | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |
| 4.4.4   | OMG   | SAMI\_1617\_run6 | 1616           | 60                | 1           | 31:36:51                    | 96    | 219.72 (380.0)             | 0.00816    | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |
| 4.4.4   | OMG   | SAMI\_1617\_run7 |                |                   | 1           | 00:00:08 - did not complete | 192   | 11.51 (512.0)              | 0          | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |
| 4.4.4   | OMG   | Wilk\_run4       | 1093           | 24                | 2           | 06:27:46                    | 288   | 249.79 (1110)              | 0.00816    | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |
| 4.4.4   | OMG   | Wilk\_run5       | 1093           | 24                | 2           | 06:11:37                    | 288   | 249.06 (1110)              | 0.00816    | [Gadi, NCI](infrastructure_optimisation_migrate_gadi.md) | 09-2020    |

</font>

## Additional notes

Any comment on major features being introduced, or default/API changes
that might result in unexpected behaviours.

# Install

  - [Gadi specific installation](infrastructure_optimisation_migrate_gadi.md) instructions.

# Tutorials

  - [Official migrate tutorial
    examples](http://peterbeerli.com/workshops/mbl/2016/tutorial)

# Help / FAQ / Troubleshooting

  - [Migrate support forum](https://groups.google.com/g/migrate-support)

# Licence

  - MIT licence in distribution README
    
        ** MIT OPENSOURCE LICENSE*****************************************************************
        *  Permission is hereby granted, free of charge, to any person obtaining a copy
        *  of this software and associated documentation files (the "Software"), to deal
        *  in the Software without restriction, including without limitation the rights
        *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
        *  of the Software, and to permit persons to whom the Software is furnished to do
        *  so, subject to the following conditions:
        * 
        *  The above copyright notice and this permission notice shall be included in all copies
        *  or substantial portions of the Software.     
        * 
        *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
        *  INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
        *  PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
        *  HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF
        *  CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE
        *  OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
        * 

# Acknowledgements / citations / credits
