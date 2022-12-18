---
jupyter:
  colab:
    toc_visible: true
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

::: {.cell .markdown id="VHdGmDRFnxwF"}
# 1 - Dependencies management {#1---dependencies-management}

***git branch name:*** dependencies
:::

::: {.cell .markdown id="mt6SsP_Ev4DQ"}
## Theory \[2\]

As usual, we will start with a few theoretical questions:

-   \[0.5\] What is Docker, and how it differs from dependencies
    management systems? From virtual machines?

Docker is a software platform that allows one to build, test, and deploy
applications quickly. Docker packages software into standardized units
called containers that have everything the software needs to run
including libraries, system tools, code, and runtime.

Docker containers are very easy to deploy in any cloud platform. It can
get more applications running on the same hardware when compared to
other dependencies management systems, it makes it easy for developers
to quickly create, ready-to-run containerized applications and it makes
managing and deploying applications much easier.

VMs (virtual machines) have the host OS (operating system) and guest OS
inside each VM. A guest OS can be any OS, irrespective of the host OS.
In contrast, Docker containers host on a ***single physical server***
with a host OS, which shares among them. Sharing the host OS between
containers makes them light and increases the boot time.

The second difference between VMs and Docker is that ***Virtual Machines
are stand-alone with their kernel*** and security features. Therefore,
applications needing more privileges and security run on virtual
machines.

Docker container packages are self-contained and can run applications in
any environment, and since they don't need a guest OS, they can be
***easily ported across different platforms***. Docker containers can be
easily deployed in servers since containers being lightweight can be
started and stopped in very less time compared to virtual machines.
:::

::: {.cell .markdown id="94BPGcghSGb9"}
-   \[0.5\] What are the advantages and disadvantages of using
    containers over other approaches?

***Advantages:***

1.  Less overhead. Containers require less system resources than
    traditional or hardware virtual machine environments because they
    don\'t include operating system images.
2.  More consistent operation. DevOps teams know applications in
    containers will run the same, regardless of where they are deployed.
3.  Flexible resource sharing.
4.  Greater efficiency. Containers allow applications to be more rapidly
    deployed, patched, or scaled.

***Disadvantages:***

1.  Difficult to manage large amount of containers.
2.  Not right for all tasks. Some applications simply need to be
    monolithic - they\'re designed that way, and benefits like
    scalability and fast deployment don\'t readily apply.
3.  Limited tools. The kind of tools needed to monitor and manage
    containers are still lacking in the industry.
:::

::: {.cell .markdown id="sPhP2oMmRsX7"}
-   \[0.5\] Explain how Docker works: what are Dockerfiles, how are
    containers created, and how are they run and destroyed?

A Dockerfile is a text document (without a file extension) that contains
the instructions to set up an environment for a Docker container. You
can build a Docker image using a Dockerfile.

Now, let\'s see how Docker containers are created, run and destroyed:

To create container first things first we have to:

\# create a directory to work in

mkdir example

cd example
:::

::: {.cell .markdown id="YPIudxlJRvB3"}
-   \[0.25\] Name and describe at least one Docker competitor (i.e., a
    tool based on the same containerization technology).

-   \[0.25\] What is conda? How it differs from apt, yarn, and others?
:::

::: {.cell .markdown id="m--WCrL11SRM"}
## Problem \[6.5\] {#problem-65}

The problem itself is relatively simple.

Imagine that you developed an excellent RNA-seq analysis pipeline and
want to share it with the world. Based on your experience, you are
confident that the popularity of the pipeline will be proportional to
its ease of use. So, you decided to help your future users and to pack
all dependencies in a Conda environment and a Docker container.

Here is the list of tools and their versions that are used in your work:

-   [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/),
    v0.11.9
-   [STAR](https://github.com/alexdobin/STAR), v2.7.10b
-   [samtools](https://github.com/samtools/samtools), v1.16.1
-   [picard](https://github.com/broadinstitute/picard), v2.27.5
-   [salmon](https://github.com/COMBINE-lab/salmon), commit tag 1.9.0
-   [bedtools](https://github.com/arq5x/bedtools2), v2.30.0
-   [multiqc](https://github.com/ewels/MultiQC), v1.13
:::

::: {.cell .markdown id="hehShsYn1Tv0"}
**Anaconda**:

-   \[1\] Install conda, create a new virtual environment, and install
    all necessary packages.
-   \[0.75\] You won\'t be able to install some tools - that\'s fine.
    List their names, and explain what should be done to make them
    conda-friendly
    ([conda-forge](https://conda-forge.org/docs/maintainer/adding_pkgs.html)
    channel,
    [bioconda](https://bioconda.github.io/contributor/workflow.html)
    channel).
-   \[0.25\]
    [Export](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-the-environment-yml-file)
    the environment
    ([example](https://github.com/nf-core/clipseq/blob/master/environment.yml))
    to the file and verify that it can be
    [rebuilt](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
    from the file without problems.

**Docker**:

-   \[3\] Create a Dockerfile for a container with **all** required
    dependencies. Don\'t forget about comments; test that all tools are
    accessible and work inside the container. Hints:
-   If needed, grant rights to execute downloaded/compiled binaries
    using chmod (`chmod a+x BINARY_NAME`)
-   Move all executables to \$PATH folders (e.g.`/usr/local/bin`) to
    make them accessible without specifying the full path.
-   Typical command to run a container interactively (`-it`) and delete
    on exit(`--rm`): `docker run --rm -it name:tag`
-   \[1\] Use [hadolint](https://hadolint.github.io/hadolint/) and
    remove as many reported warnings as possible.
-   \[0.5\] Add relevant
    [labels](https://docs.docker.com/engine/reference/builder/#label),
    e.g. maintainer, version, etc.
    ([hint](https://medium.com/@chamilad/lets-make-your-docker-image-better-than-90-of-existing-ones-8b1e5de950d))
:::

::: {.cell .markdown id="k7BfQC_m1CFU"}
## Extra points \[1.5\] {#extra-points-15}

You will be awarded extra points for the following:

-   \[0.5\] Using [multi-stage
    builds](https://docs.docker.com/build/building/multi-stage/) in
    Docker. E.g. to build STAR and copy only the executable to the final
    image.

-   \[0.75\] Minimizing the size of the final Docker image. That is,
    removing all intermediates, unnecessary binaries/caches, etc. Don\'t
    forget to compare & report the final size before and after all the
    optimizations.

-   \[0.25\] Create an extra Dockerfile that starts from [a conda base
    image](https://hub.docker.com/r/continuumio/anaconda3) and builds
    everything from your conda environment file.

Hint: `conda env create --quiet -f environment.yml && conda clean -a`
([example](https://github.com/nf-core/clipseq/blob/master/Dockerfile))
:::

::: {.cell .markdown id="HLwL-s8Poji_"}
# General requirements

**Works that fail to follow the below requirements won\'t be graded.**
:::

::: {.cell .markdown id="5FF6nI1Aoslb"}
## How to submit the homework?

All homework must be submitted as a link to a public git repository
(preferably GitHub/GitLab). In addition, you must complete each task in
a separate branch with a particular name (see each section).
:::

::: {.cell .markdown id="eHk8RyUErT2-"}
## What is the reporting format?

Reports should be provided as markdown README files in the root folder
of the git repository. Please, use markdown features to make the report
easy to read, e.g., you must include code in special blocks, use
headings, etc.

You are strongly advised to write in English, but usage of Russian
won\'t be penalized (except for code comments, see below).

Reports should be self-contained, i.e. include all code
(bash/dockerfiles/etc), explanations, and illustrations (e.g.
screenshots). Ideally, to evaluate your assignment and reproduce
results, I would only need the README file and nothing else.

It is a must to comment your code and explain what is happening in each
code block. You must write code comments in English.
:::

::: {.cell .markdown id="SrCQrX1svRf1"}
# Resources
:::

::: {.cell .markdown id="Rr8yuVHcvVe8"}
-   [Git immersion](http://gitimmersion.com/) - a popular git course
:::
