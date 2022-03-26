# teletype_mols

**Update**

> For an unknown reason, GitHub is no longer displaying the molecule printed ascii within the Jupyter Notebook, however, you can view the entire ascii output online using the Jupyter nbviewer interface: [rdkit_print_mol_ascii on nbviewer](https://nbviewer.org/github/vfscalfani/teletype_mols/blob/main/rdkit_print_mol_ascii.ipynb)

This is a work in-progress and mostly for fun because I like to print molecules in the terminal.
Below are two very basic methods that have worked for me.

While the below methods achieved my initial goals of printing a molecule as ascii characters, 
I haven't yet been able to figure out how to make the printing of the molecules more compact with either method, 
while maintaining a reasonable aspect ratio (i.e., molecule printing gets distorted if a lot smaller). 
If you have any feedback on how to 'shrink' the molecules, it would be greatly appreciated.

## Method 1: Using RDKit

[RDKit](https://www.rdkit.org/) includes the [Schroedinger 2D coordinate generation library](https://github.com/schrodinger/coordgenlibs) 
(CoordGen) and this can be used to get the x,y coordinates of atoms and bonds for plotting.

The [rdkit_print_mol_ascii](https://github.com/vfscalfani/teletype_mols/blob/main/rdkit_print_mol_ascii.ipynb) notebook in this repository 
demonstrates one way of printing molecules as ascii characters using RDKit.

The `print_mol_ascii` function is likely most useful in an ipython console to quickly view molecules (i.e., not in a full Jupyter Notebook). 
Eventually I would like to adapt the script into a python argparse command line application for use in a terminal window, more generally.

Here is an example of how molecules look. Atoms are printed with their standard symbols, and bonds are denoted with a `*`:

```console

                                                        Br                            
                                                                                     
                                                        *                            
                                                                                     
                                                        C                            
                                                    *       *                        
                                                C               C                    
                                                                                     
                                                *               *                    
                                                                                     
                C               N               C               C                    
            *       *       *       *       *       *       *       *                
        C               C               C               C               Br            
                                                                                     
                                                                                     
        *               *                               *                            
                                                                                     
                                                                                     
        C               C                               N                            
    *       *       *                                                                
O               C                                                                    
                                                                                                                                                                                    
                                                                                                 
```

## Method 2: Using gnuplot

[gnuplot](http://www.gnuplot.info/) can plot as ascii characters in a terminal window. So if you have atom/bond xy coordinates either from RDKit or
some other toolkit, it's fairly straightforward to plot them using gnuplot. The bond coordinates below are the center xy positions of the bond. 
Note that the y direction is flipped from the example above:

```console
$ cat mol2_atoms
156.596602856445	262.888402526855	C
125.485403515625	281.00359967041	C
94.2446039550782	263.118802307129	C
94.1150092285156	227.118799560547	C
125.226203076172	209.003601043701	C
156.474204174805	226.888399780273	C
187.578201977539	208.780400054932	N
218.819004284668	226.67240032959	C
249.930203625488	208.557200439453	C
281.178204724121	226.44919934082	C
312.282205273438	208.334000823975	C
312.159806591797	172.334000823975	C
280.911802746582	154.442000549316	C
249.807804257202	172.557200439453	C
280.782205273437	118.449202087402	Br
343.530200878906	226.218799560547	Br
281.307804943848	262.442000549316	N
63.1333991210938	281.226797912598	O

```

```console
$ cat mol2_bonds
141.041003186035	271.946001098633
109.865003735352	272.06120098877
94.1798065917969	245.118800933838
109.670606152344	218.061200302124
140.850203625488	217.946000411987
172.026203076172	217.834399917603
203.198603131104	217.726400192261
234.374603955078	217.614800384522
265.554204174805	217.503199890137
296.730204998779	217.391600082397
312.221005932617	190.334000823975
296.535804669189	163.388000686646
265.359803501892	163.499600494385
280.84700401001	136.445601318359
327.906203076172	217.276400192261
281.243004833984	244.445599945068
78.6890015380859	272.172800109863
156.535403515625	244.888401153564
249.869003941345	190.557200439453

```

```console
$ gnuplot -e "set term dumb; \
> unset xtics; unset ytics; unset border; \
> plot 'mol2_atoms' using 1:2:3 with labels notitle, \
> 'mol2_bonds' using 1:2 with points pt '*' notitle"

                                                                               
  O               C                                                            
      *       *       *                                                        
          C               C                                N                   
                                                                               
          *               *                                                    
                                                           *                   
                                                                               
          C               C                C               C              Br   
              *       *       *       *        *       *       *       *       
                  C               N                C               C           
                                                                               
                                                   *               *           
                                                                               
                                                   C               C           
                                                       *       *               
                                                                               
                                                           C                   
                                                                               
                                                           *                   
                                                                               
                                                          Br                                                                                          

```                                                                          
                                                                          
## Other recent efforts I found that print molecules as ascii characters:

1. [Noel O'Boyle's ascii format in Open Babel](https://baoilleach.blogspot.com/2012/04/depict-chemical-structurewithout.html)
2. [drewberryants asciiMOL - curses based ascii molecule viewer](https://github.com/dewberryants/asciiMol)

## Literature references related to teletype molecule printing

1. Carhart, R. E. A Model-Based Approach to the Teletype Printing of Chemical Structures. J. Chem. Inf. Model. 1976, 16 (2), 82–88. https://doi.org/10.1021/ci60006a011.
2. Feldmann, R. J.; Koniver, D. A. Interactive Searching of Chemical Files and Structural Diagram Generation from Wiswesser Line Notation. J. Chem. Doc. 1971, 11 (3), 154–159. https://doi.org/10.1021/c160042a008.
3. Thomson, L. H.; Hyde, E.; Matthews, F. W. Organic Search and Display Using a Connectivity Matrix Derived from Wiswesser Notation. J. Chem. Doc. 1967, 7 (4), 204–209. https://doi.org/10.1021/c160027a005.










