# Configuration Management for

# Clinical Ancillary Product Line 

## VistA MUMPS Code

VistA MUMPS Code starts with the platinum version of code.

## Branches

--- Describe what a branch is ---

### Main - Long Lived

Created from the Platinum/Gold(??) version of the product

### Dev - Long Lived

Branch from created from main

### Patch - Short Lived

Branch from Dev; Named according to the Patch being worked on using the "Patch-*" convention

Created as needed and deleted when finished

When Patch is committed back to Dev it should be tagged with an [annotated tag](#tags) 

### Hot Fix - Short Lived

Branch from Dev; Named according to the defect being addressed using the "Fix-*" convention where the JIRA Tag for the defect is part of the name (e.g. Fix-1356)

### Pre-Prod - Short Lived

Branch from Dev after Patch has been merged back into Dev

Used for Final IOC testing



---

*Notes:* 
*Protect the branches - Settings; Branches;* 
*Default branch should be production branch*
*Branch Protection Rules*
*Require PR Reviews before merging*
*Dismiss stale pull request approval when new commits are pushed*
*Establish status checks then require status checks to pass before merge*
*Include Administrators*
*wild card rule for branches with a name pattern*
*release-\* <-- Any branch starting with "release-\**
*Manage Access* 

---

## Commits

*Commit often, push to origin regularly (ideally at the end of every day)*

Commits save changes to the local repository after the changes have been staged. In order to save the changes a commit message needs to be added to describe the changes made.

When using the Git command line tool to add a commit message use the `-m` option.

Commit messages can be as simple as one line, or as complex as necessary with a subject line giving a high level overview of what is being committed

```
$ git commit -m "Derezz the master control program"
```

If subject and body are needed (highly recommended):

```
$ git commit
```

Git will launch the default text editor (which can be set by the `git config --global` command)

Every commit must contain a commit message which corresponds to the good commit guidelines specified for the team.

### Good Commit Message Guidelines

Commit messages should be clear and meaningful.

A well-crafted Git commit message is the best way to communicate context about a change to other developers working on that project.

Commit messages can adequately communicate why a change was made, and understanding that makes development and collaboration more efficient.

Properly written commit messages can significantly help to analyze the history of changes to the code.

[Bad commit](https://medium.com/better-programming/stop-writing-bad-commit-messages-8df79517177d) messages can confuse and obfuscate changes made that other developers or auditors may not be able to understand when reviewing code history.

- Every commit message should have 3 parts:
  - Subject - Describe the commit in a short imperative tense sentence fragment (followed by a blank line)
  - Body - More detailed description of the commit which can be multiple paragraphs and include standard markdown (if the commit is small enough the body may not be needed as the subject should be informative enough)
  - Closing - Additional useful meta-data (JIRA ticket numbers, additional reference links, additional developers information)
- Specify the type of commit using a Standard Terminology for the subject line


| First Word | Meaning                                              |
| ---------- | ---------------------------------------------------- |
| Add        | Create a capability e.g. Patch, test, dependency.    |
| Bump       | Increase the version of something e.g. dependency.   |
| Chore      | Regular code maintenance                             |
| Cut        | Remove a capability e.g. Patch, test, dependency.    |
| Docs       | Anything related to documentation                    |
| Patch      | Anew Patch being added to a particular application   |
| Fix        | Fix an issue e.g. bug, typo, accident, misstatement. |
| Make       | Change the build process, or tooling, or infra.      |
| Optimize   | Refactor of performance, e.g. speed up code.         |
| Refactor   | A code change that MUST be just a refactoring.       |
| Reformat   | Refactor of formatting, e.g. omit whitespace.        |
| Start      | Begin doing something; e.g. create a Patch flag.     |
| Stop       | End doing something; e.g. remove a Patch flag.       |
| Style      | Patch and updates related to styling                 |
| Test       | Anything related to testing                          |

- Subject lines must never contain (and / or start with) anything that is unique to the application or system (that goes in the body of the commit message.)
- Do not end the subject line with a period
- Capitalize the subject line and each paragraph

- Separate individual paragraphs in the body with a blank line
- Bullet points can be used in the body (a hyphen or asterisk preceded by a single space and blank lines in between bullet points)
- Commit message should not contain any whitespace errors
- Remove unnecessary punctuation marks
- Use the imperative mood in the subject line (think of the subject line as the completion of the following sentence: *"If applied, this commit will..."*)
- Use the body to explain what changes you have made and why you made them

- Do not assume the reviewer understands what the original problem was, ensure you add it

- Do not think your code is self-explanatory

- Issue/JIRA tracking references should be put at the bottom of the commit body


| First Word | Meaning                                                      |
| ---------- | ------------------------------------------------------------ |
| Resolves   | Issue # referenced has been fixed by developer               |
| Closes     | Issue # referenced her been confirmed fixed by QA            |
| See Also   | Issue #'s referenced refer to other issues this commit addresses |

Sample commit message with subject and body:

```
Derezz the master control program

 - MCP (Master Control Program) has been derezzing other programs
 
 - MCP has been usurping system resources and denying user requests
 
MCP turned out to be evil and had become intent on world domination.
This commit throws Tron's disc into MCP (causing its deresolution)
and turns it back into a chess game.

Resolves: #123
Closes: #1570
See also: #456, #789
```

---



  ## Tags

A tag is a way to mark a point in time in the repository. Typically tags are used to mark a release version of the repository. [Tags are not the same as branches](https://en.wikibooks.org/wiki/Git/Advanced#:~:text=The%20difference%20between%20tags%20and,and%20usually%20not%20be%20changed).

While there are 2 types of tags (lightweight and annotated), annotated tags should always be used. Lightweight tags simply list the [semantic version](https://semver.org/) of the release (or in the case of VistA a tag can be the VistA patch # *Note: VistA patches do not make use of the [Semantic Versioning](https://semver.org/) standard*) while annotated tags give not only the version of the release but also who created the tag, when it was created (which may or may not be the same person/date of the branch it's pointing to) and any message (similar to a commit message) the tagger attributed to the tag. For more information on Git Tagging, check out the [Git Basics Tagging](https://git-scm.com/book/en/Git-Basics-Tagging) page.

giving a high level overview of what is being committed (Patch # and Test Version #)

```
$ git tag -a DG-5.3-342-V4 -m "Both DG-5.3-342 and XYZ-1-100 are mutually dependent upon each other"
```

If no message is specified for an annotated tag:

```
$ git tag -a DG-5.3-342-V4 -m
```

 then Git will launch the default text editor (which can be set by the `git config --global` command). 

```
$ git tag -a XYZ-1-100-V1 -m "Both DG-5.3-342 and XYZ-1-100 are mutually dependent upon each other"
```

*In the case of patches being dependent upon other patches the patch installation sequence # should be added to the tag as well????* ***NO - Because Seq# does not change per code changes***



## Repository Folder Structure

Readme.md (see [Example](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/va-mobile-app/README.md))

Testing (see [Example](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/va-mobile-app/testing))

### Roles

*Note: All roles listed and defined in the Application Team's Readme*  

Product support release coordinator...

- Application Coordinator (AC) - Owner of the main branch - Responsible for approving/merging code back into main branch upon national release

  - Also owner of the dev branch - Responsible for approving/merging code back into dev branch prior to IOC testing

- Team Lead (TL) - responsible for oversight and management of the overall development process of the patch

- Lead Developer (LD) - Responsible for ensuring the PDRC and SDRC are completed and included in the "CheckList" folder, Coordinating with LD's of other overlapping patches.

  The LD is also responsible for creating the "short lived" patch branch as well as verifying  changes before issuing a pull request to merge the changes back into dev upon completion of the development changes.

- SQA Manager - Responsible for ensuring the proper Test Definition documents (see [Example](https://github.com/department-of-veterans-affairs/va.gov-team/tree/master/products/va-mobile-app/testing)) in the Applications "Test" folder

and the code is ready for SQA testing, 

## VistA/MUMPS Development Process examples

### Example 1. Single Patch

In working on a single patch the **lead developer** should create a stub patch in FORUM (See: National Patch Module Guide for details) which provides the Patch # to be used.

- Updating the defects status of the appropriate problem ticket(s) in JIRA (or project tracker of choice).

A Patch branch from the current Dev branch and named according to convention (*Patch-\**) using the Patch # generated by NPM (National Patch Module). 

Developers can then checkout that Patch branch to their local development environments *(Question: What IDE's are common for current developers. Should we reference the most common ones and docs on how to do a checkout/check in for those IDE's)* and proceed with their normal development process. 

Exporting of the source from the developer's VistA environment into external files for inclusion into a Git repository and performing regular commits (see [Good Commit Guidelines](#Commit Guidelines)) back to their local branch should be performed and a push back to the GitHub repository should be done on a daily basis at minimum. 

Once development of the components of the patch have been completed, a KIDS build needs to be generated and exported and added to the local Patch branch. 

The developer should complete the Primary Developer Review Checklist (PDRC) and include this in the test folder in the Patch branch of the local repository. If appropriate the Secondary Developer Review Checklist (SDRC) should be completed and added to the test folder as well.

At this point the Patch branch should be tagged with an annotated tag (see [Tags](#tags)), containing the Patch # and Test Version # 

```
$ git tag -a DG-5.3-342-V1 -m "Add first test version of this patch"
```

Patch-tracking message (See: National Patch Module Guide for details) sending the message on FORUM to test sites and the appropriate Product Support Release Coordinator. 

*Prior to merging the changes back into main, the final thread of the Patch-tracking message be stored in GitHub.*

*Prior to merging the changes back into main, the final thread of the Release Message should also be stored in GitHub.*

The VistA SQA Checklist should be updated for each test version and be included in the test folder of the patch.

![Single Patch](README.assets/Single%20Patch.svg)

In committing the addition of the KIDS build to the local Patch also tag the commit with an annotated tag which should include the Patch Number as well as the Test Version (see [Tags](#tags)).

Once committed and pushed to the GitHub repository, a Pull Request should be made to merge the current changes into the Dev branch. Once the changes have been merged into Dev the code should be sent to FORUM for testing by SQA.











### Example 3: Two patches from different packages must be installed together for both to function properly

   If two patches have to be installed together, create them in a combined build. For example XYZ-1-100 and DG-5.3-342 are mutually dependent upon each other. Each would be in it's own Patch Branch (Patch 1 and Patch 2 in the diagram below). Which would need to be merged as part of SQA prior to testing.

   NOTE: Combined builds should be used judiciously. Combining multiple patches that depend on one specific patch but not on each other may create risks in testing and deployment. When doing a combined build, consultation with the ***Release Coordinator*** is required. If uncertain, consultation with a ***package expert*** is warranted.



![Mutually Dependent Patches](README.assets/Mutually%20Dependent%20Patches.svg)



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

   