 CBM Firmware Repository
=======================

This repository contains the source code for all firmware used in the
CBM experiment.

Repository Access
-----------------

The repository can be accessed using either SVN directly or GIT via
the git-svn bridge (substitute your GSI Web Login name for *xxx*):

    $ svn co --username xxx https://subversion.gsi.de/cbmsoft/firmware/trunk firmware
    $ git svn clone --username=xxx -s https://subversion.gsi.de/cbmsoft/firmware

Read access is open to all CBM collaborators.

Commits should only be performed by the person responsible for the
respective design or component, or by his or her representative. (This
is presently not enforced by SVN, so please act responsibly. If you
mess up the repository, you will generate lots of work for other
people.)

Repository Contents
-------------------

The initial structure of the repository is:

    ├── cores
    │   ├── cbm_net
    |   └── ...
    ├── designs
    |   ├── roc3
    |   └── ...
    └── tools

The `cores` directory contains subdirectories for each major design
core that is used by several different designs. This should not
include minor cores like FIFOs or RAM blocks, which should be placed
within the respective cores or designs.

The `designs` directory contains subdirectories for each major
firmware design project.

In addition, a `tools` directory is foreseen for generic scripts and
tools that cannot be attributed to a specific core or design.

Some general guidelines for the contents of the CBM firmware repository:

- **Include all sources and scripts**  
  To ensure that a firmware image can be modified and rebuilt at a
  later time, all sources and scripts required to build the firmware
  image should be included in the repository.

- **No generated or unused files**  
  Files that can be automatically generated only clutter the
  respository and should not be committed. The same applies to source
  code files that are not used in the project.

- **No binary files**  
  In general, large binary (i.e., non-text) files should not be
  committed as they are not handled well by SVN.

- **Use trunk, tags and branches**  
  Stick to the standard use of the SVN structure of trunk, tags and
  branches. In general, most branches should be temporary and merged
  with the trunk at some point.

- **Avoid the _svn:externals_ property**  
  The repository should directly contain all required sources. Using
  SVN Externals complicates the repository structure and causes
  compatibility problems.

Source Code Quality
-------------------

The code uploaded into this repository should meet the quality
standards generally associated with **production** or **testing
level** code.

The repository is meant as a platform for source code exchange between
the groups involved and as an archive for CBM. It is not meant to
replace a developer's local version control system and should not
contain early development code or code that does not
compile/sythesize.
