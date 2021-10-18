# SwitchMiDesigner

## Description

SwitchMi Designer is a tool developped to design toehold switch that target small RNA sequences such as microRNA. Toehold switches are de-novo-designed-riboregulators that are  composed  of  two strands  of  RNA. Firstly,  the  switch  strand  contains a single stranded sequence at the 5’ end that is followed by the hairpin module upstream the repressed gene. The hairpin  module  includes  the  ribosome binding site  (RBS) in the loop of the hairpin and the start codon (AUG). The repressed  gene  encodes  for  a  colorimetric,  fluorescent, or  electrochemical  measurable  output.  
The  other  RNA strand of the toehold switch is the trigger RNA that binds 
to  the  toehold  sequence  thanks  to  Watson-Crick  base pairing,  enabling  the  opening  of  the  hairpin,  then  the exposition of the RBS site and start codon, leading to the translation of the coding gene previously repressed. 

![](Figures/Design%20principle%20of%20toehold%20switch.jpg)

SwitchMi Designer is based on the [Toeholder](https://github.com/igem-ulaval/toeholder) developed by the the ULaval iGEM Team in 2019. It is working on target RNA longer than 30 base pairs (bp), but a microRNA is usually between 18 and 23 bp. To adress this limitation, We adapted to the new version 4.0 of NUPACK and modified it, allowing the use of microRNA as target. Verification of the final product, the protein produced when the RNA is bound to the Toehold Switch, was also added.

For further information, please refer to our [webpage](https://2021.igem.org/Team:UParis_BME).

## Dependencies 

The following program must be installed :

[NUPACK](http://www.nupack.org) (Zadeh et al. 2011. Journal of Computational Chemistry)

Scripts also depends on the following Python libraries:

- [Biopython](https://biopython.org) (Cock et al. 2009. Bioinformatics)
- [NumPy](https://numpy.org)
- [Pandas](https://pandas.pydata.org)
- Os
- Csv 

Templates and examples also use the [easygui](https://easygui.readthedocs.io/en/master/) library.

## Scripts
All scripts are written in Python 3 and depend on the previous libraries.

- [SwitchDesigner_main_function.py](/SwitchDesigner/SwitchDesigner_main_function.py): Contains the SwitchMi Designer function that can be used in a implemented in a script (like in Example_script.ipynb) or in an automated script (Example_automated.py). SwitchMi Designer sweeps through the miRNA sequence to find suitable candidate recognition sequences. Toehold sequences are then generated and tested to verify the absence of stop codon and the viability of the protein. 

- [SwitchDesigner_helper_functions.py](/SwitchDesigner/SwitchDesigner_helper_functions.py): Contains several helper functions for the SwitchDesigner_main_function script.

## Input

The workflow is fully automated to be executed as follows as long as all the scripts are in the current directory:

```
parameters ={"input_seq":'/path/gene_name.fasta', 
             "output_folder":'/path/output_folder_name',
             "len_unpaired":10,
             "len_paired":4,
             "reporter":'ATGCGTAAA',
             "mol_type":'RNA',
             "min_unpaired":4,
             "suitable_aa":["L","F","Y","I","N","K"]}
             
SwitchDesigner(parameters)             
```

The parameters dictionnary must contain all the necessary adjustable variables for the script, including:
- Path to the input sequence (FASTA formatted)
- Path to the output folder
- Length of the unpaired region of the recognition sequence 
- Length of the paired region of the recognition sequence
- Reporter gene or tag to be added to the end of the toehold
- Input sequence molecule type (DNA or RNA)
- Minimum number of unpaired bases in the secondary structure of the target mRNA for a candidate trigger to be considered
- List of suitable amino acids wanted for the first amino acid in the protein


## Output

The SwitchMi Designer function returns a dataframe identical to the .csv file called "selected_toeholds_results" detailed below. 
The function also generate an output folder named after the miRNA chosen. A first .csv file called "toehold_candidates" is created, containing all miRNA sequences that had the requirements (2 weak pairs/ 1 strong pair at the hairpin base and minimum 4 unpaired bases), with the following informations : 
- Non paired count
- Structure
- Sequence
- Start
- End	
- Length unpaired trigger	
- Length paired trigger 

Toehold sequences are generated and tested to verify the following modalities : absence of a stop codon and stability of the beginning of the protein. A second .csv file called "selected_toeholds_results" is created and contains the following informations : 
- Non paired count in the miRNA subsequence
- Structure	of the miRNA subsequence
- Sequence	
- Start	position
- End	position
- Length unpaired trigger	
- Length paired trigger	
- Index	
- Binding energy of toehold + mRNA	
- Binding energy of toehold only	
- Binding energy of mRNA only	
- GC content	
- Protein sequence 

Apart from those .csv files, the rest of the files are .txt files containing the sequence of each toehold selected, either in DNA or RNA.

## Templates

The folder [Templates](/Templates) contains two python scripts with the SwitchDesigner function ready to be used.

## Examples of results obtained with SwitchDesigner

The folder [Results example](/Results%20example) contains different results obtained with the SwitchMi Designer function.
