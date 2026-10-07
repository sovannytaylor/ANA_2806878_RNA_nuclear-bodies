# ANA-XX_brief-description

*Advice for use*: This repository uses core scripts managed in a separate repository ([punctalyze](https://github.com/ocarmo/punctalyze)) to promote modularity and code reuse across projects in the Boeynaems lab. The checklist below outlines the steps to initiate an experiment repository in a tidy manner and add the analysis submodule. The punctalyze module is under heavy construction, any changes should be committed in a non-breaking manner, as they link to the main branch. Please check off the tick boxes with an 'x' as you go. This repository assumes elementary knowledge of python and git.

### if you have not already forked the punctalyze repository:
- [ ] fork the core pipeline if you have not already
        visit the [punctalyze](https://github.com/ocarmo/punctalyze) and click **"Fork"**
        this gives you a personal copy at `https://github.com/YOUR_USERNAME/punctalyze`
- [ ] clone your fork locally by clicking **"<>Code"** at the top right of the GitHub page, then **"Open with GitHub Desktop"**
- [ ] select your local path and open the repo by clicking the **"open in VS Code"** option
- [ ] continue to the checklist below

### if you already forked punctalyze: make your own image analysis repo
- [ ] click the **"Use this template"** button at the top right of this template repository
- [ ] name your project and click **"Create repository from template"**
- [ ] clone onto your local device
- [ ] open this repository (which you just cloned) in VS Code or your editor of choice
- [ ] uncomment raw_data folders in gitignore 
- [ ] delete placeholder files raw_data folders
- [ ] import the editable analysis submodule in vscode terminal
~~~ 
git submodule add https://github.com/YOUR_USERNAME/punctalyze.git punctalyze 
~~~
^^^ this adds your forked 'punctalyze' pipeline to this experiment repository
~~~ 
git submodule add -b branch_name https://github.com/YOUR_USERNAME/punctalyze punctalyze 
~~~
^^^^ this adds your forked 'punctalyze' pipeline to this experiment repository, specifically the branch specified with '-b <branch_name>'

- [ ] navigate to the submodule and add a new branch unique to this analysis (if you don't already have one)
~~~
cd punctalyze
git checkout -b dev_branch_name
~~~
- [ ] update *header* at top of README.md and *experiment details* below
- [ ] upload raw data, or update the input_path in ```1_initial_cleanup.py```

## Experiment details

**Purpose**: 
Detecting and analyzing intracellular puncta from light micrographs

**Cell Type**: 
Neuro2a cells

**Instrument/techniques**: 
LSM900, experiment block set up, 10% excitation for 40.51 sec, acquisitions at mCh 0.6% 600V.

**Data produced:** 
See results folder

**Analysis:** 
- scrape data from online if necessary
- initial wrangling of images into numpy arrays
- cell segmentation
- segmentation validation
- detecting puncta (foci of high-intensity pixels) and extracting feature information per punctum
- averaging puncta feature information per cell
- plotting

## General git/submodule workflow schematic
```
experiment repo
   └── submodule → your fork
            └── feature branch → active hacking
```            

## Making contributions to punctalyze
### if you make changes to your fork that you want to merge to the main branch at [punctalyze](https://github.com/ocarmo/punctalyze):
```
feature branch
   ↓ PR
boey-lab/punctalyze (upstream)
```
checklist if preferred:
- [ ] push your commits in VS Code source control or terminal
- [ ] go to your fork on GitHub
- [ ] click Compare & pull request
- [ ] set the base repo to original-owner/repo and the base branch to main
- [ ] write a description of your changes
- [ ] click Create pull request

Thanks for using and contributing to punctalyze! Your improvements help make image analysis easier for everyone. If you have any questions, feel free to open an issue or contact the maintainer.

## Synching punctalyze
### to keep your fork synced with the original punctalyze:
```bash
git remote add upstream https://github.com/ocarmo/punctalyze.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```


### if you want to update punctalyze inside your pipeline project, and you're not contributing changes to it, run:
```bash
git submodule update --remote --merge
git commit -am "Update submodule to latest punctalyze commit"
```
