# osm-series4-synthesis-round1

This is a follow-up of the previous work on generating new candidates for the [Open Source Malaria project](https://github.com/opensourcemalaria). Plase follow the thread [#34](https://github.com/OpenSourceMalaria/Series4_PredictiveModel/issues/34) on the OSM GitHub page as well as the associated repos for [Round1](https://github.com/ersilia-os/candidates) and [Round2](https://github.com/ersilia-os/osm-series4-candidates-2) to get an overview of what has been done in this project so far.

## Zairachem Predictive Model
We base the selection of the best candidates for experimental synthesis on a predictive model trained using our automated ML pipeline [ZairaChem](https://github.com/ersilia-os/zaira-chem). To benchmark the ML model, we reproduced the original competition for series 4 activity prediction recently published ([Tse et al, 2021](https://pubs.acs.org/doi/abs/10.1021/acs.jmedchem.1c00313)). The Zairachem-trained model was able to predict correctly 30 out of the 33 molecules in the list (using 2.5 uM as a threshold for activity).
We subsequently retrained the pipeline with all available data (original training set + competition molecules + newest synthesized molecules).

## New generation of candidates based on high-actives
Using the methodology described by the [ETH Modlab](https://github.com/ETHmodlab/virtual_libraries) for low data generative models, we generated 772 new series 4 molecules using for transfer learning the best experimentally validated molecules (IC50 <= 1) (89 molecules) and the best molecules from Round 2 (90 molecules)

## Selection of potent candidates
We merged the 772 new molecules with the set of 17800 molecules from Round 2 and predicted their activity with the ZairaChem model. The results of this prediction can be found in the data folder.
