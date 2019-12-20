# Table of contents

This is a short guide about how to use the [PaccMann GUI](https://sysbio.uk-south.containers.mybluemix.net/paccmann) and what is happening behind the curtain.

- [PaccMann GUI Guide](#paccmann-gui-guide)
    - [Purpose of PaccMann](#purpose-of-paccmann)
    - [Purpose of PaccMann GUI](#purpose-of-paccmann-gui)
    - [Walkthrough](#walkthrough)
    	- [Getting-started](#getting-started)
        - [Input](#input)
            - [SMILES](#smiles)
            - [Molecule Editor](#molecule-editor)
            - [Cancer cell-lines](#cancer-cell-lines)
        - [Output](#output)
        	- [Result Table](#result-table)
            - [Visualization](#visualization)
            - [Download](#download)
    - [Known issues](#known-issues)
    - [Tested browsers](#tested-browsers)
    
    


## Purpose of PaccMann

`PaccMann` acronyms **P**rediction of **A**nti**C**ancer **C**ompound sensitivity with **M**ultimodal **A**ttention-based **N**eural **N**etworks.

The purpose of the project is to develop an user-friendly and interpretable interface to perform in-silico IC50 drug screenings for cancer cell lines. The screening is performed from the combination of a chemical compound and the transcriptomics profile of the cell line of interest.

The purpose of the PaccMann GUI is to provide a PaccMann pipeline from input to result as an easy to use service for the community.




## Walkthrough

### Getting started

Access the service by clicking `Start` on the [main page](https://sysbio.uk-south.containers.mybluemix.net/paccmann).
![The login ensures your data is kept private.][login]

### Input

#### SMILES
The UI prompts the user with two fields, for the compound and the name of the cancer cell line respectively.
![The default input screen.][input]

Chemicals are represented as SMILES (`Simplified Molecular Input Line Entry System`) sequences, i.e. an inline text notation for molecules. This 1D abstraction is obtained by a molecular graph traverse resulting in a list of atoms, bonds and meta-symbols.

For example the TKI Masitinib (commercial name Masivet) can be represented as:
`CC1=C(C=C(C=C1)NC(=O)C2=CC=C(C=C2)CN3CCN(CC3)C)NC4=NC(=CS4)C5=CN=CC=C5`

Services such as [PubChem](https://pubchem.ncbi.nlm.nih.gov) can help to retrieve the SMILES sequence of known chemicals.

The user can fill the field with a chemical of interest and run the model by clicking `Predict`. After a little while and upon success, the page refreshes itself and lets the user inspect all results with interactive plots or download the results as `.csv` file by pressing.

#### Molecule editor
If the user is unfamiliar with SMILES, or prefers to draw the molecules directly, the  molecule editor offers a user-friendly way to explore and test molecules interactively.
The molecule editor can be opened by clicking `Toggle molecule editor` and offers various functionalities. 
![The molecule editor][molecule_editor]

The left panel contains the tools for editing the molecule, e.g. the `erase tool` (to erase specific atoms or bonds), the `bond tool` (to add a bond from a set of typical bonds), the `ring structure tool` (to add a ring from a set of typical rings) and the `atom and formula tool` which allows to insert new atoms.
Upon finishing the drawing, the user **has to confirm the molecule by clicking the grey check button** at the bottom of the left panel.

The tools at the top panel allow the user to import own data from a variety of formats including `.smi`, `.mol`, `.cml`, `.kcj`, `.rxn`, `.json` and others. Upon finishing the molecule design the user can alternatively simply download and export the molecule into one of the aforementioned formats.

#### Cancer cell-lines
Next to the SMILES string of the compound, the **transcriptomics profile (bulk RNA-Seq)** of the cancer cell line of interest is given as input to the model.
The backend has access to all **970 cell lines from the [GDSC panel](https://www.cancerrxgene.org)**.
Each cell line is represented through the transcriptomics profile of 2128 preselected genes following a propagation procedure over a PPI network.
The **set of 2128 genes** used for the predictions can be seen [here](https://ibm.ent.box.com/s/vfehvfly7mi2obvaj86pjuy9a82e8nik/file/489488390168).



### Output
#### Result table
Per default, the predictions are performed for .

![Result for running PaccMann on 960 cell lines with Embelin][results_embelin]

On success of the task the results are presented in a interactive table with the following columns: 
* `Rank`: Ranks the cell lines. Rank 1 shows the cell line with the highest predicted efficacy.
* `Attended Genes`: Shows in descending order the 5 genes mostly contributing to the model's decision.
* `Cell line`: Shows the name of the cell line according to the GDSC panel.
* `Histology`: Shows the histological information of the cancer cell line.
* `Micromolar IC50`: Shows the predicted IC50 score for the (drug, cell-line) pair.
* `Site`: Shows the tissue origin of the cell line.

In this case, Embelin is predicted to be most effective on `SIG-M5` which is a cell line of `Haematopoietic and lymphoid` tissue. The top-5 most attended genes are `FBX034`, `TSN`, `NNAT`, `KPNA7` and `CST1`.

The table can be sorted in ascending or descending order by every column. The columns can also be filtered by tpying a string of interest, e.g. in order to search for the result of a specific cell line or show the predictions for all cell lines of a tissue type. 
The width and the vertical ordering of the columns may also be changed according to the user's preferences.



#### Download 
This interactive (filtered) table can be downloaded by clicking the blue `Download CSV` button at the bottom of the results section.


#### Visualization
A heatmap plot of the molecule is shown at the top right. It visualizes the **attention distribution** of the network and highlights the **molecular substructures most relevant for the prediction**. Lighter colors correspond to less relevance, whereas darker colors indicate a high importance.
This attention heatmap is different for every (drug, cell-line) pair. However for the visualization presented in the UI, we average all 960 attention profiles. In this case it can be seen that the carbon chain tail as well as the oxygens attached to the 5-ring were most relevant for the prediction.



## Known issues

If you receive the following error while opening the [PaccMann website](https://sysbio.uk-south.containers.mybluemix.net/paccmann): 
```
{"error":"invalid_client","error_description":"prompt : none is supported only for single page application"}
```
One of the following will fix the problem:
- Opening the service in a fresh, private browser window
- Wipe your browser cookies

## Tested browsers

The preferred browser for `PaccMann_aas` is Firefox.
Here is a complete table for the browsers and OS with verified functionality.

|OS   	|   Chrome	|   Edge	|   	Safari|  Firefox 	|
|---	|---	|---	|---	|---	|
| Linux  	| &#x2611;  	|   N.A.	|  N.A. 	|  &#x2611;	|
| Windows	| &#x2611;  	|   	|  N.A. 	|&#x2611;   	|
| MacOS  	| &#x2611; 	|  N.A. 	| &#x2611;  	|  &#x2611; 	|

[login]: paccmann_gui/screens/login.png
[input]: paccmann_gui/screens/input_screen.png
[molecule_editor]: paccmann_gui/screens/molecule_editor.png
[results_embelin]: paccmann_gui/screens/result_embelin.png
