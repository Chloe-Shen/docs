---
permalink: /
---

# PaccMann UI

This is a short guide about how to use the [PaccMann UI](https://sysbio.eu-gb.containers.appdomain.cloud/paccmann-aas-gui) and what is happening behind the curtain.

## Purpose of PaccMann

`PaccMann` acronyms **P**rediction of **A**nti**C**ancer **C**ompound sensitivity with **M**ultimodal **A**ttention-based **N**eural **N**etworks.

The purpose of the project is to develop an user-friendly and interpretable interface to perform in-silico IC50 drug screenings for cancer cell lines. The screening is performed from the combination of a chemical compound and the transcriptomics profile of the cell line of interest.

The purpose of the PaccMann UI is to provide a PaccMann pipeline from input to result as an easy to use service for the community.

## Tutorial

### Getting started

Access the service by clicking `Start` on the [main page](https://sysbio.eu-gb.containers.appdomain.cloud/paccmann-aas-gui).
![The cookies ensure your data is kept private.][start]

The home page will present to the user a form to input data and submit predictions.
![PaccMann home page][home]

### Input

PaccMann supports two type of inputs: molecules and gene expression data.

#### Molecules

Chemicals are represented as SMILES (`Simplified Molecular Input Line Entry System`) sequences, i.e. an inline text notation for molecules. This 1D abstraction is obtained by a molecular graph traverse resulting in a list of atoms, bonds and meta-symbols.

For example the TKI Masitinib (commercial name Masivet) can be represented as:
`CC1=C(C=C(C=C1)NC(=O)C2=CC=C(C=C2)CN3CCN(CC3)C)NC4=NC(=CS4)C5=CN=CC=C5`

Services such as [PubChem](https://pubchem.ncbi.nlm.nih.gov) or
[ZINC](http://zinc.docking.org/substances/) can help to retrieve the SMILES
sequence of known chemicals.

The user can have more information on the SMILES handling we perform by clicking the corresponding info button.
![Smiles info][smiles_info]
![Smiles info expanded][smiles_info_expanded]

The user can fill the SMILES field with a chemical or select molecules from a dropdown menu.
![Drug dropdown][drug_selection]

If the user is unfamiliar with SMILES, or prefers to draw the molecules directly, the  molecule editor offers a user-friendly way to explore and test molecules interactively.
The molecule editor can be opened by clicking `Molecule Editor` and offers various functionalities.

The user can  even edit drugs after selection, just pick a molecule in the dropdown.
![Selected drug][bax_selection]

And open the editor.
![Drug editor][bax_editor]

The left panel contains the tools for editing the molecule, e.g. the `erase tool` (to erase specific atoms or bonds), the `bond tool` (to add a bond from a set of typical bonds), the `ring structure tool` (to add a ring from a set of typical rings) and the `atom and formula tool` which allows to insert new atoms.
![Adding ring][bax_editor_ring]

Upon finishing the drawing, the user **has to confirm the molecule by clicking the grey check button** at the bottom of the left panel.
![Confirm molecule][bax_editor_confirm]

The tools at the top panel allow the user to import own data from a variety of formats including `.smi`, `.mol`, `.cml`, `.kcj`, `.rxn`, `.json` and others. Upon finishing the molecule design the user can alternatively simply download and export the molecule into one of the aforementioned formats.

By clicking the button `Done` the user can go back to the submission page.

#### Omic data

The user can provide custom data for the prediction. An example can be downloaded from [here](https://ibm.box.com/v/paccmann-aas-data). In case the user does not provide data the prediction will be performed on all the cell lines from the GDSC (v2) and CCLE studies. Keep in mind this might take up to 5 minutes.
No worries, the service run predictions in an asynchronous fashion and use cookies to leave the user session open, so that there is no need to leave the browser tab open.

Information on the genes supported by the model can be accessed via the info button.
![Genes information][genes_info]
![Genes information expanded][genes_info_expanded]
The omic data should be provided as `.csv` with genes in the columns and one row
per cell line. The order of the columns does not need to adhere to the order we
provide in our example and additional genes are discarded. Missing genes are
mean-imputed (with 0s).

The **set of 2128 genes** used for the predictions can be also donwloaded
[here](https://ibm.ent.box.com/s/vfehvfly7mi2obvaj86pjuy9a82e8nik/file/489488390168).


#### Condifence estimate

Additionally PaccMann provides the possibility to associate a confidence value to its estimates.
![Confidence estimate information][confidence_info]

Once the parameters are set the form is ready for submission.
![Submission ready][submission]

By pressing the `Predict` button the user will submit a PaccMann job and, upon completion, a `Results` button will appear allowing the user to analyse and visualise the data.
![Results ready][results_ready]

### Results

#### Result table

The predictions are rendered in an interactive and downloadable containing IC50 estimate, the confidence is requested and metadata if provided in the uploaded CSV.

![Result for running PaccMann][sensitivity]

The table can be sorted in ascending or descending order by every column. The columns can also be filtered by tpying a string of interest, e.g. in order to search for the result of a specific sample or show the predictions for all samples of a tissue type.
The width and the vertical ordering of the columns may also be changed according to the user's preferences.
This interactive (filtered) table can be downloaded by clicking the blue `Download CSV` button at the bottom of the results section.

#### Attention visualization

The bottom part of the page shows the attention results. On the left a heatmap for the molecule provided with a colorbar shows parts of the molecule attended when performing the predictions. On the right attended genes are shown.
By default the average over the considered samples is reported.
![Attention average][attention_average]

The gene visualization allows to use a slider to show any given number of top attended genes.
![Attention gene slider][attention_average_gene_slider]

Different samples can be selected via a dropdown rendering different attention profiles for specific samples.
![Attention for sample 1][attention_sample_1]

Drug attention plots can be downloaded in vector graphic format in a zip file.
[attention_sample_1_download]: paccmann_gui/screens/attention_sample_1_download.png

Gene attention plots can  be downloaded using the tools embedded in the visualization.

## Tested browsers

The preferred browser for [PaccMann website](https://sysbio.eu-gb.containers.appdomain.cloud/paccmann-aas-gui) is Firefox.
Here is a complete table for the browsers and OS with verified functionality.

|OS   	|   Chrome	|   Edge	|   	Safari|  Firefox 	|
|---	|---	|---	|---	|---	|
| Linux  	| &#x2611;  	|   N.A.	|  N.A. 	|  &#x2611;	|
| Windows	| &#x2611;  	|   	|  N.A. 	|&#x2611;   	|
| MacOS  	| &#x2611; 	|  N.A. 	| &#x2611;  	|  &#x2611; 	|

[start]: paccmann_gui/screens/start.png
[home]: paccmann_gui/screens/home.png
[drug_selection]: paccmann_gui/screens/drug_selection.png
[smiles_info]: paccmann_gui/screens/smiles_info.png
[smiles_info_expanded]: paccmann_gui/screens/smiles_info_expanded.png
[genes_info]: paccmann_gui/screens/genes_info.png
[genes_info_expanded]: paccmann_gui/screens/genes_info_expanded.png
[confidence_info]: paccmann_gui/screens/confidence_info.png
[bax_selection]: paccmann_gui/screens/bax_selection.png
[bax_editor]: paccmann_gui/screens/bax_editor.png
[bax_editor_ring]: paccmann_gui/screens/bax_editor_ring.png
[bax_editor_confirm]: paccmann_gui/screens/bax_editor_confirm.png
[submission]: paccmann_gui/screens/submission.png
[results_ready]: paccmann_gui/screens/results_ready.png
[attention_average]: paccmann_gui/screens/attention_average.png
[attention_average_gene_slider]: paccmann_gui/screens/attention_average_gene_slider.png
[attention_sample_1]: paccmann_gui/screens/attention_sample_1.png
[attention_sample_1_download]: paccmann_gui/screens/attention_sample_1_download.png
