# CRISPY template (modified CRISP-DM)

This repository contains a cookie-cutter Python repository for the CRISPY workflow. CRISPY is a workflow 
based on CRISP-DM, but modified in certain places to improve practicality. Please refer to the repository 
this template is based on for more information: [crisp-dm-template](https://github.com/MichaelVerdegaal/crisp-dm-template)

CRISPY is a data science workflow, meaning that it describes a process specific for 
executing data science projects. Such processes are becoming more necessary the more 
data science experiments you run, as they are highly iterative in nature, and can be messy when left unorganized. 
Traditional software engineering workflows aren't always applicable to data science, which brings up the need for
dedicated workflows.

## Changes from the original

The original CRISP-DM workflow is a great starting point, but it has some flaws that significantly 
detract from my personal experience using it. These changes are so significant that i've not found it proper to 
include them the original template repository, and i consider this a custom workflow instead. This workflow may 
update over time, and be less backwards compatible than the original. Major changes can be found below.

### Removal of the deployment phase
Personally, i rarely found the deployment phase to be used. This is the phase where, in case of a positive 
evaluation, and the goals have been met, it’s discussed how the model should be implemented. I personally 
attribute two separate reasons: 
- In case that the goals were not met, the deployment phase is not filled in, leaving you with the template text.
- Even if the goals were met, this phase requires you to have finished the research, and then to at a later date 
finish writing it, as it requires you to write a post-mortem on how the deployment went.

To solve this, without completely removing this action, the user is now required to create a deployment plan 
at the end of phase 5, if their evaluation is sufficiently favorable.

### A data collection plan for the data understanding phase
In phase 2 you will start initial data collection, and perform surface-level data analysis. 
The issue here is that this collection process is left up to the user, and there’s no 
guidelines for them to hold onto regarding it. This can result in vastly different data-criteria per 
experiment, and in the worst case, lead to faulty conclusions due to improper data collection.

To solve this, in phase 2 you can now find extra tasks, that require you to describe how you will
collect your data. While this may introduce extra work, it will also prevent you from making mistakes 
in phase 3 and onwards in relation to data quality issues.

### Text revisions
In certain places, the text has been revised to be more clear, or to improve the readability of the document.  As a 
result, the consequent text output of may differ from the intent of the original text. Some examples of this are:
- removing the project plan section in the business understanding phase
- moving the terminology section in the business understanding phase to the beginning of the document
- taking into account singular models in the modeling phase

### Source folder trimming
After use, i found that the source folder was not used as much as intended. While this idea is still good, 
i consider the user responsible enough to figure out themselves when to move code to a separate file, and in 
what manner to do so.

## This repository

This repository contains the following folders for you to use.

```text
crisp-dm-template
---data | datasets for your experiment
    ---raw | datasets in the form you'll receive them without further modification
    ---processed | datasets at the end of the data preparation stage, if applicable
---docs | phased notebooks to write your experiment report in
---source | insert python code that is used to help produce your report, if applicable
```

Using the template is simple.

1. Click the "Use this template" button on the top right of the repository to create a new repository.
2. Set up a new virtual environment, and install the packages with `poetry install`, courtesy of 
the [poetry](https://python-poetry.org/) package manager.
3. Run `pre-commit install` to install the pre-commit hooks, which will help you keep your code clean.
4. Follow the steps in `docs`, to write your experiment report. Get assistance from the source material of CRISP-DM 
5. in case of trouble writing the text.

## Notes

### What kind of functions should `source` contain?

A good generic rule is to move code to a new function in `source` if:
- You reuse a piece of code more than once
- A piece of code is considerably lengthy, and detracts from the reading experience in docs
- A piece of code requires extra documentation/context to be properly understood

### What if i need an extra file/folder?

An important consideration for this repository is that it's supposed to be flexible, it's a 
template in the end. As such, if your specific experiment requires say, an extra folder in `data` 
to stay organised, then don't feel afraid to do so. After all, this template is 
modified from the original for a good reason.

**However**, it is important that these changes are made with consideration, for the sake of 
consistency. No one wants your experiments to have a different structure for every single 
experiment, as this makes it substantially harder to find the right information. As such, if you make 
a modification to the template, please make sure your team is aware of it.

### Why Python specific?

Python is by far the most popular language for data science purposes, which myriads of online sources could confirm. Due to the popularity and personal preferences the decision has been made to primarily tailor this template towards Python, however, just because this is the focus, that doesn't mean you can't use the template in another language. In case you want to switch programming languages, take these steps:

1. Remove poetry related files (poetry.lock and pyproject.toml).
2. Remove python files in `source`, and switch the file type to the desired language choice.
3. Update the pre-commit packages (or remove it entirely)
4. Add the steps necessary to reproduce the project environment in your language of choice.
5. Make sure to include any packages necessary to get the Jupyter Notebooks to run.

In case your language somehow doesn't support Jupyter Notebooks ([which is pretty difficult)](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels), then you'll have to do more manual labor. The notebooks are filled with markdown text, which you'll have to extract from the notebooks cells (text inside the `#%% md` blocks)to another suitable file format.

