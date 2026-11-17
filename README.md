# HBB CRISPR Target Finder

## Question
Where could CRISPR-Cas9 cut the human HBB gene close to the mutation that causes sickle cell disease?

## Background
Sickle cell disease is caused by a single DNA letter change in the HBB gene, which codes for part of hemoglobin. The codon GAG becomes GTG, so the amino acid glutamic acid is replaced with valine.

## Method
1. Downloaded the human HBB mRNA sequence (NM_000518) from NCBI using Biopython.
2. Extracted the protein-coding sequence and translated it to check that the protein starts MVHLTPEEKS.
3. Located the codon for the glutamic acid that mutates, and made a mutant copy to confirm GAG to GTG gives E to V.
4. Searched for NGG PAM sites within 30 letters of the mutation.
5. For each site, recorded the 20-letter guide, the cut distance from the mutation, and the GC content.

## Results

| Position | Guide (20 letters) | PAM | Cut distance | GC % |
|----------|--------------------|-----|--------------|------|
| 51 | GCAACCTCAAACAGACACCA | TGG | -21 | 50.0 |
| 69 | CATGGTGCATCTGACTCCTG | AGG | -3 | 55.0 |
| 95 | AGTCTGCCGTTACTGCCCTG | TGG | 23 | 60.0 |
| 96 | GTCTGCCGTTACTGCCCTGT | GGG | 24 | 60.0 |
| 97 | TCTGCCGTTACTGCCCTGTG | GGG | 25 | 60.0 |

**Best guide:** CATGGTGCATCTGACTCCTG (PAM AGG), cutting 3 letters from the mutation with 55% GC.

**Why I chose it:** *I chose the guide at position 69 (CATGGTGCATCTGACTCCTG, PAM AGG) because Cas9 would cut only 3 letters from the sickle cell mutation. The other four guides cut 21 to 25 letters away. Its GC content is 55%, which is inside the usual 40-60% range, but all five guides were in or near that range, so cut distance was what decided it.*

## Limitations
- I used the mRNA sequence, not the full genomic DNA with introns.
- I searched only one strand of the DNA.
- I did not check for off-target matches elsewhere in the genome.
- TODO: check whether this guide works on both the normal and the sickle cell version.

## What I learned
*I learned that DNA is read in groups of three letters, so the DNA sequence is about three times longer than the protein it codes for, and that changing one letter can change an amino acid, as in sickle cell disease. I also learned how Cas9 needs a PAM (NGG) next to its target, and that I could estimate how often one appears by chance (about 1 in 16). The hardest parts were debugging a one-character typo in the NCBI ID (a hyphen instead of an underscore) and learning that Colab forgets everything when it disconnects, so I need to run all the cells again. Next time I want to check for off-target matches, which this project doesn’t do.*

## Tools
Python, Biopython, Google Colab
