

## Misc

Then a new  Dev branch is created by the development team leader with a tag specific to the JIRA Story/Defect

The development team leader should also monitor the Main branch for any changes made by other development teams and pull any changes down to the Dev branch and inform the rest of the team of the changes.

![Single Patch Old](D:/Users/Administrator/Documents/dbITPro%2520-%2520Projects/10_2020_CAP%2520CM/tmp_CM/README.assets/Single%2520Patch%2520Old.svg)

From the new  Dev branch a   Patch/Fix branch is created and tagged according to the JIRA task #

Developers working on the Patch should clone the repository and make any necessary code changes in their local development environment. Committing and pushing those changes up to the repository on a daily basis. 

Developers must also monitor the Patch/Fix branch prior to pushing code up (fortunately git will warn of any changes in the branch you're trying to push to) for any changes made by an upstream branch by another team.

Once the Patch/Fix branch changes have been made and tested any changes made to the  Main branch should be pulled down to the Patch/Fix branch and retested.

Once the code is ready for testing it should be pushed into FORUM by the development team leader from the Dev branch. At the same time an SQA branch is created from the Dev branch and tagged with the test version of the code and the current Main branch semantic version.



![Single Patch Old  2](D:/Users/Administrator/Documents/dbITPro%2520-%2520Projects/10_2020_CAP%2520CM/tmp_CM/README.assets/Single%2520Patch%2520Old%2520%25202.svg)





If, during SQA testing any defects are discovered a new tag must be added to the Patch/Fix branch for the JIRA Task # assigned to the defect. Once the defect is fixed a new pull request is issued up to the Dev branch, and the changes are pushed to and merged into the existing SQA branch for testing as well

A KIDS build based on the Dev branch is loaded into FORUM.

![Single Patch Old  3](D:/Users/Administrator/Documents/dbITPro%2520-%2520Projects/10_2020_CAP%2520CM/tmp_CM/README.assets/Single%2520Patch%2520Old%2520%25203.svg)

Once SQA has given final approval of the Patch/Fix, a new Release branch is created from the Dev branch. The code is pulled from FORUM for PreProd/IOC testing and when approved a pull request is issued from the Release branch back into the Main branch.

Pull request reviewed by Dev team and Application Coordinator.



Upon successful release the Dev, Patch/Fix, SQA, and Release branches are deleted from the repository















**Pull:** Pull changes from an upstream repository into your own local repository

**Pull Request:** is a request for an upstream repository to pull changes from your repository into that upstream repository





KIDS build:

routines

Create a MD file for each task, outlining what the task is, who is responsible for each component (e.g. Testing, Pull Requests from each branch, etc see the )



https://github.com/department-of-veterans-affairs/va-mobile-app

https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/va-mobile-app

https://gist.github.com/PurpleBooth/b24679402957c63ec426

https://github.com/nasa/openmct/blob/master/CONTRIBUTING.md

https://www.contributor-covenant.org/version/1/4/code-of-conduct/

https://gist.github.com/allthedoll/76b36afa687b2e0a424a7851919830b8 - Readme template





-------------------------------------------------

1. Start with "main" - "gold" instance
2. Long duration "Dev" tagged with 

## Current VistA Development Process

This is the series of steps I have taken in the past. Please note that it might be that GitHub is a straightforward replacement for Rational in these steps, but I’m not entirely sure; we’ll need to discuss it after you’ve had time to consume this tome:

1. As a developer on a new project, I am given access to several VistA instances for development:
   *(The names in parentheses are the namespaces we used for the VSR project.)*

A “gold” instance for use in comparing to the  development instance. (PATVEE) - **GitHub Main Branch**



1. 1. A main development instance (“main”) where I make my changes. (MNTVBB) - **GitHub Patch Branch** - Branched off of "Dev" branch and given name "Feat-\*"  (e.g. Feat-DG-5.3-964)

   2. Developer would check out this branch into their development environment

   3. Do dev work and commit/push changes regularly with commit messages

      When ready for SQA Testing, create a build via KIDS - 

      **Export KIDS build into flat file** with new **test version number**

      Add the KIDS build Export to the Patch Branch and commit back to Dev with an annotated tag briefly what this build is for

      Commit comment should be brief about the changes made in this commit:

  Load Build into FORUM
  Send to SQA

   


   Example 2: also needs merging

   **Example 3: Two patches from different packages must be installed together for both to function properly.**
   If two patches have to be installed together, create them in a combined build. For example XYZ-1-100 and DG-5.3-342 are mutually dependent upon each other. Each would be in it's own Patch Branch (Patch 1 and Patch 2 in the diagram below). Which would need to be merged as part of SQA prior to testing.

   NOTE: Combined builds should be used judiciously. Combining multiple patches that depend on one specific patch but not on each other may create risks in testing and deployment. When doing a combined build, consultation with the ***Release Coordinator*** is required. If uncertain, consultation with a ***package expert*** is warranted.

   Gold version is all packages

OLD VERSION VVVVVVVVVVVVVVVVVVVVVVVVVV

![2Patches](D:/Users/Administrator/Documents/dbITPro%2520-%2520Projects/10_2020_CAP%2520CM/tmp_CM/README.assets/2Patches.svg)

OLD VERSION ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^





![Mutually Dependent Patches](D:/Users/Administrator/Documents/dbITPro%2520-%2520Projects/10_2020_CAP%2520CM/tmp_CM/README.assets/Mutually%2520Dependent%2520Patches.svg)



Patch 1 branch devs work on package DG (Registration name space)

Patch 2 branch devs work on package XU (Kernel Name space)

As each patch is developed in their own Patch branch commits and pushes back into the remote repository need to be properly commented (see [Good Commit Guidelines](#Commit Guidelines))

Issue pull requests for each patch Commit changes to the Dev branch adding an appropriate commit message (see [Good Commit Guidelines](#Commit Guidelines)), (Note: leave out the '-m' to use default editor to create a more detailed commit message)

```
Patch XYZ-1-100> git add .
Patch XYZ-1-100> git commit -m "Add KIDS build"
Patch XYZ-1-100>
```

Add an annotated tag to the commit then push that [specific tag](https://stackabuse.com/git-push-tags-to-a-remote-repo/) to the remote


```
Patch XYZ-1-100> git tag -a XYZ-1-100 -m "Patch XYZ-1-100 ready for initial Test #1234; Requires Patch DG-5.3-342"
Patch XYZ-1-100> git push Repo-Name XYZ-1-100

```

Use `git tag -n` to show all tags and their messages

```
Patch XYZ-1-100> git tag -n
XYZ-1-100       Patch XYZ-1-100 ready for initial Test #1234
XYZ-1-101       Patch XYZ-1-101 Ready for initial test. Test version # 1

Patch XYZ-1-100>
```

Use `git log` to show commit messages

```
Patch XYZ-1-100>git log
commit e6eea1146287dc5a6e14d6f4df51657bef98f436 (HEAD -> main, tag: XYZ-1-100)
Author: michael-barlow3 <michael-barlow3@va.gov>
Date:   Tue Nov 3 17:05:09 2020 -0500

    Start first commit of locally modified data
    
    Modified the initial Readme.md

commit 57d928cea97c90178745c54f7ce916b94254dbcd (origin/main, origin/HEAD)
Author: michael-barlow3 <michael-barlow3@va.gov>
Date:   Mon Oct 26 13:31:20 2020 -0400

    Add KIDS build
Patch XYZ-1-100>
```

   



```
Patch DG-5.3-342> git commit -m "Add KIDS build"
```


```
Patch DG-5.3-342> git tag -a -m "Patch DG-5.3-342 implemented Test Version 3"
```

   

   

   

   

   

   

   

   

   

   

   

      1. An instance (“primary”) for testing the patch installation as part of the Primary checklist. (TSTVSR)
      2. An instance (“secondary”) where another developer installs the patch for the Secondary Developer checklist. (TSB)
      3. Perhaps another “gold” instance for use in comparing to the secondary developer’s instance. (GLD)

   4. I create the stub of a patch for the particular package in FORUM, which assigns the next patch number available.

   5. I confirm1 that “main” is up-to-date with the latest patches.

   6. I edit my changes in “main.”
      *(This is the daily process we followed in the VA FileMan 22.2E project):*

   7. 1. Lock and download the routine (<NAME>.m file) from the Rational source stream repository.
      2. Compare the routine with “main” to make sure there were no differences.
      3. Make my changes.
      4. Export the routine to a sequential file.
      5. Upload the routine to Rational.
      6. Unlock the routine in Rational.

   8. I perform unit testing of my changes in “main.”

   9. I use the KIDS (Kernel Installation and Distribution System) to create the patch in “main.”

   10. I update the patch with all the components I am modifying (Data Dictionaries, Routines, Menu Options, etc.).

   11. I modify the Patch Description, following the template guidelines, in the FORUM patch.

   12. If the patch contains more than just routines3, I may also need to write a separate routine (which may evolve into a separate patch that may be needed by VA Support to install on client instances if the initial patch needs to get rolled back).

   13. I export the patch from “main” and test the installation in “primary.”

   14. I perform additional unit testing in “primary.”

   15. I repeat steps 4-11 until I am satisfied with the results.

   16. I follow the steps outlined in the National Patch Module (NPM) Guide to send the patch from “main” to FORUM and update the patch in FORUM and assign a Test Version number.

   17. I fill out the Primary Developer Review Checklist (PDRC).

   18. I send the patch from FORUM to the secondary developer.

   19. The secondary developer tests the patch installation, reviews the code and tests the patch Patches/fixes, reporting any findings in the Secondary Developer Review Checklist (SDRC).

   20. If necessary, I repeat steps 4 through 16 until the secondary developer and I are satisfied.

   21. I send the patch from FORUM to the SQA team.

   22. The SQA team completes the SQA Checklist, checking the routines for proper formatting, and the code for proper behavior, etc.

   23. I repeat steps 4-19 until the SQA team is satisfied with the results.

   24. Typically, we wait until now to upload the artifacts to the appropriate repository:

   25. 1. The Patch Description in a Word document.
        2. The PDRC, SDRC and SQA Checklist.
        3. The Patch (KIDS Build) exported from “main” as a host file.

   26. We go to IOC testing.

   27. If the site reports any problems, then I repeat steps 4-21 until the site is satisfied with the results.

   28. The site installs into production and we cross our fingers.

   29. If issues are found in production, it may be necessary to create an emergency patch (with a category of “PATCH FOR A PATCH”) to fix the issue.

----------

1 There are multiple ways to confirm, such as asking whomever provided the environment, or painstakingly checking the installed patches against the list of released patches in FORUM.

2 There are two ways to export the patch: 1) by a PackMan (Package Manager) message sent by MailMan (Mail Manager) from “main” to “primary,” or 2) by creating a host file where “main” is located, and if necessary, transferring the file to the system where “primary” is located.

3 There is an existing path to follow for backing out a patch that contains only routines. That procedure is documented in the Patch Description template.

 





- Good [description](https://stackoverflow.com/questions/49414218/difference-between-tag-and-commit-message#answer-49415064) of difference between tag and commit name/message



## Questions

Each CAP has it's own repository.



**Question:** Is there a GitHub repository for the CAP line itself? Something that contains an over view of the entire product line (see [va.gov-team](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/va-mobile-app) )? You could even include the [CA_PLM-Forever](https://github.com/department-of-veterans-affairs/Clinical-Ancillary_PLM-Forever) issue as part of it and not have a separate repository just for the forever tickler

In such a repository each product would have it's own 

See the [team folder](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/va-mobile-app) for all the background, discovery, planning, and decisions that preceded application development.

and particularly things which should be common to all products in the CAP Line, for example:

- [Accessibility](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/platform/accessibility)

**Question:** Does the team make use of Slack channels for alerting of processes which GitHub can report on?



Products within the CAP Line can fall into 2 basic categories, MUMPS and non-MUMPS code

Both of which are, by necessity, developed differently.

[GitHub Repository Naming Convention](https://github.com/department-of-veterans-affairs/configuration-management/wiki/3.04-GitHub-Repository-Naming-Convention)

Configure the repository as outlined in the [VA Repository Settings](https://github.com/department-of-veterans-affairs/configuration-management/wiki/3.06-Configuring-Repository-Settings) guide

This is a test comment by Keith Avery.