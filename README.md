# Book of abstracts for FEniCS Conference 2024

This repository contains the source code for generating the Book of Abstracts for the FEniCS conference 2024 (June 12-14) in Oslo.

Presenters that submit abstracts to the FEniCS conference 2024 do this through a Google form which in turn can be downloaded as a `.csv` file. Here we take this `.csv` file and generate one individual MarkDown file as a [MyST Scientific PDF](https://mystmd.org/guide/creating-pdf-documents). Next, we generate PDFs from these markdown files using a [custom template](https://mystmd.org/jtex/create-a-latex-template) that is found in the [`template`](template) folder.

## Installation instructions

You need to install

- Python (https://www.python.org/downloads/)
- Node (https://nodejs.org/en/download)
- Latex (https://www.latex-project.org/get/)

Once this is installed you can install the dependencies by first creating a virtual environment

```
python3 -m venv venv
```

activate it

```
. venv/bin/activate
```

and install the dependencies

```
python -m pip install .
```

## Generating fake data

If you don't have the `.csv` file available you can generate a `.csv` with fake abstracts using the command

```
python3 generate_fake_abstracts.py <file> <N>
```

e.g

```
python3 generate_fake_abstracts.py abstracts.csv 10
```

which will create 10 fake abstracts in the file `abstract.csv`. Note that the `csv` file has the following fieldnames

```
"Username",
"Abstract title",
"Abstract text",
"Name of authors (including presenter, comma-separated list)",
"Affiliation of co-authors (including presenter, comma-separated list)",
"Reference list"
```

## Converting `csv` file to MarkDown

To convert the `.csv` file to individual markdown files you can run the command

```
python3 convert.py abstracts.csv
```

which will put each the abstracts in the folder `book/abstract` (you can also specify the output folder with the `-o` flag)

## Online version of the book of abstract

If you go into the `book` folder

```
cd book
```

and run the command

```
myst start
```

you should be able to go to `localhost:3000` to see the online version of the book.

## Creating PDFs

In the online version, it is also an option to download each abstract separately. In order to be able to download the abstracts as PDF we need to first generate the PDFs with MyST. To do this first go to the `book` folder

```
cd book
```

and run the command

```
myst build --pdf
```

This will create one pdf for each abstract

### Merge all abstracts together

One thing you might want to do is to download all abstracts in one go. We have created a script to merge all the pdfs together into one large pdf which can be downloaded from the landing page (i.e the README page). To merge all the pdfs together you can do

```
python3 merge-abstracts.py
```

After retarting the `myst` server (`myst start`) you should now be able to also download the abstracts as PDFs

## Deploy site

Please checkout out the workflows in [`.github/workflows`](.github/workflows) folder to learn how this can be deployed to GitHub pages.

## Organizing committee

- Jørgen Dokken
- Henrik Finsberg
- Marie Rognes
