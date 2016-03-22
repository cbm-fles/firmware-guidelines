CBM Firmware Repository Guidelines
==================================

The CBM firmware repository collection contains the source code for
all firmware used in the CBM experiment.


Repository access
-----------------

Read access is open to all CBM collaborators.

Commits should only be performed by the person responsible for the
respective design or component, or by his or her
representative. Contributions from other developers are welcome and
should be handled via pull requests.


Firmware structure
------------------

The Firmware is structured into `cores` and `designs`. Purpose of this
structure is to provide defined interfaces between sub-projects with a
minimal set of rules.

A core is a major building block that is used by several different
designs. This does not include minor cores like FIFOs or RAM blocks,
which may be part of a core or a design. For each core an interface
documentation and an example design should be provided.

A design is a major firmware design project. A design may include
cores as well as other sources.

For each component (design/core) a separate git repository may
exist. A repository may also contain several components if they are
closely related. Cores can be included into design repositories via
the `git submodule` functionality.


Build results
-------------

Each firmware component must support fully automated builds.

Builds for cores should result in synthesized netlists and matching
constraints. Designs containing the respective core include these
netlists/constraints during their build flow.

Builds for designs should result in FPGA bitfiles and PROM files if
applicable.


Automated build flow
--------------------

The following conventions should be followed to facilitate the
implementation of a continuous integration service:

- In each repository, an executable file named `autobuild` should
  exist at the top level. Invoking this file without command line
  arguments should execute all necessary steps for a complete build. A
  return code of zero from this file should indicate a successful
  build including a check that all constraints were met.

- The final build results (netlist/bitfile) should be placed in a
  directory `result` at the top level of the repository. There must be
  no subdirectories. The file names should not be volatile, i.e., they
  should not contain version or date/time information. In general, the
  toplevel netlist or bitfile should have the same base name as the
  repository.

- Additional output and log files relevant for later analysis should
  be copied to a `report` directory at the top level of the
  repository.


General guidelines for the contents of the CBM firmware repositories
--------------------------------------------------------------------

- **Include all sources and scripts**  
  To ensure that a firmware image can be modified and rebuilt at a
  later time, all sources and scripts required to build the firmware
  image should be included in the repository.

- **No generated or unused files**  
  Files that can be automatically generated only clutter the
  repository and should not be committed. The same applies to source
  code files that are not used in the project.

- **No binary files**  
  In general, large binary (i.e., non-text) files should not be
  committed as they are not handled well by version control.

- **Use only temporary branches**
  Stick to the standard use of branches. In general, branches should
  be temporary and merged with the master at some point. Tags can be
  used to label specific versions.


Source code quality
-------------------

The repositories are meant as a platform for source code exchange
between the groups involved and as an archive for CBM. The code
uploaded into the repository master branch should meet the quality
standards generally associated with **production** or **testing
level** code. It should not contain early development code or code
that does not compile/synthesize.
