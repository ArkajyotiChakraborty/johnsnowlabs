---
layout: docs
comment: no
header: true
seotitle: NLP Lab | John Snow Labs
title: Import Documents
permalink: /docs/en/alab/import
key: docs-training
modify_date: "2020-11-18"
use_language_switcher: "Python-Scala"
show_nav: true
sidebar:
  nav: annotation-lab
---

Once a new project is created and its configuration is saved, the user is redirected to the **Import page**. Here the user has multiple options for importing tasks.

<img class="image image__shadow" src="/assets/images/annotation_lab/4.2.0/import.png" style="width:100%;"/>

Users can import the accepted file formats in multiple ways. They can drag and drop the file(s) to the upload box, select the file from the file explorer, provide the URL of the file in JSON format, or import it directly from the S3 bucket. To import from Amazon S3 bucket the user needs to provide the necessary connection details (_credentials_, _access keys_, and _S3 bucket path_). All documents present in the specified path, are then imported as tasks in the current project.

<img class="image image__shadow" src="https://user-images.githubusercontent.com/46840490/203529045-14df3352-e8c5-4a7d-9f3a-e152c51e6d43.gif" style="width:100%;"/>

## Plain text file

When you upload a plain text file, only one task will be created which will contain the entire data in the input file.

This is an update from earlier versions of Annotation Lab when the input text file was split by the new line character and one task was created for each line.
{:.warning}

## Json file

For bulk importing a list of documents you can use the json import option. The expected format is illustrated in the image below. It consists of a list of dictionaries, each with 2 keys-values pairs (“text” and “title”).

```bash
[{"text": "Task text content.", "title":"Task title"}]
```

## CSV, TSV file

When CSV / TSV formatted text file is used, column names are interpreted as task data keys:

```bash
Task text content, Task title
this is a first task, Colon Cancer.txt
this is a second task, Breast radiation therapy.txt
```

## Import annotated tasks

When importing tasks that already contain annotations (e.g. exported from another project, with predictions generated by pre-trained models) the user has the option to overwrite completions/predictions or to skip the tasks that are already imported into the project.

<img class="image image__shadow" src="/assets/images/annotation_lab/4.2.0/overwrite.png" style="width:100%;"/>

> **NOTE:** When importing tasks from different projects with the purpose of combining them in one project, users should take care of the overlaps existing between tasks IDs. Annotation Lab will simply overwrite tasks with the same ID.

## Dynamic Task Pagination

The support for pagination offered by earlier versions of the Annotation Lab involved the use of the `<pagebreak>` tag. A document pre-processing step was necessary for adding/changing the page breaks and those involved extra effort from the part of the users.

Annotation Lab 2.8.0 introduces a paradigm change for pagination. Going forward, pagination is dynamic and can be configured according to the user’s needs and preferences from the Labeling page. Annotators or reviewers can now choose the number of words to include on a single page from a predefined list of values or can add the desired counts.

<img class="image image__shadow" src="/assets/images/annotation_lab/4.2.0/pagination.gif" style="width:80%;"/>

A new settings option has been added to prevent splitting a sentence into two different pages.

<img class="image image__shadow" src="/assets/images/annotation_lab/2.8.0/158552636-1b9f8814-5e05-4904-8ab4-401ea476d32e.png" style="width:60%;"/>
