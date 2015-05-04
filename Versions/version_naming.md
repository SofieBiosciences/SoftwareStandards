SofieBio Version Naming Standards
========================

Purpose
-------

   - All software developed, including software developed in the R&D prototype phase,
     should be tracked in source control.
   - The version numbers will track each software change.
   - Each change should be a deliberate change that can be tracked back to a design or product requirement.
   - The software’s primary purpose is to encourage workflow,
     therefore lines of code should be treated like bolts in SolidWorks.

Version Numbers
---------------

   - **Three number system (1.2.3)**
   - **First number notes major releases(1.x.x)**
      * Iterations in this number likely indicate significant changes in
        hardware / software that notes incompatibility.
      * Also can indicate significant feature implementation,
        i.e. a major release can be comprised of a single standard release.
      * For customers under service contract using old versions,
        bugs will not be fixed in old versions if they are already fixed in the most recent version.

   - **Second number notes standard releases**
      * These are any releases that are made available to customer sites.
      * Each standard release is made up of many individual revisions that represent a single software change.
      * Each software feature should be versioned as standard release.

   - **Third number notes revisions**
      * One revision notes one change, e.g. it can be one bug fix or an iteration of feature

Source Control
--------------

   - All working and complete versions of software need to be submitted to a source control tool regularly.

   - Source control will not only contain our software, but also all of the binaries and installers
     we need to run the software.  When available, we also need submit source code for any dependency
     as well, e.g. open source libraries we may use.  The reason for this is that we need to be able to reproduce
     a working version of software from scratch independent from any other outside entity,
     provided we have the proper licenses.
     If Ubuntu Linux dissolves, we want to be able to continue to update our software.

   - Previously, projects coming from UCLA have been stored on public GitHub repositories.
     This is no appropriate for any development we do that is not in itself an open source project.
     Our source code should be stored on a private repository with access controls.


Release Installers
------------------

   - Software releases will be hosted so that it is available externally to the necessary parties,
     including distributors and partner companies.
   - The site will have access control so that we can grant access.  It will not be publicly available.
   - Will be identified by the version number, and will contain any installers, scripts,
     and other items that are necessary for an update or install.
   - Intended for the download folder to be transferred to a USB stick (or any other medium) for install.

Release Notes
-------------

   - There will be release notes included with every software release.
   - Notes can be in the form a text file included at the top level folder.
   - Notes should contain a description of all software fixes that can be expected.