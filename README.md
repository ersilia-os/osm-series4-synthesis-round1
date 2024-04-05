# osm-series4-synthesis-round1

This is a follow-up of the previous work on generating new candidates for the [Open Source Malaria project](https://github.com/opensourcemalaria). Plase follow the thread [#34](https://github.com/OpenSourceMalaria/Series4_PredictiveModel/issues/34) on the OSM GitHub page as well as the associated repos for [Round1](https://github.com/ersilia-os/candidates) and [Round2](https://github.com/ersilia-os/osm-series4-candidates-2) to get an overview of te previous work.

## Zairachem Predictive Model
We base the selection of the best candidates for experimental synthesis on a predictive model trained using our automated ML pipeline [ZairaChem](https://github.com/ersilia-os/zaira-chem). To benchmark the ML model, we reproduced the original competition for series 4 activity prediction recently published ([Tse et al, 2021](https://pubs.acs.org/doi/abs/10.1021/acs.jmedchem.1c00313)). The training and test set for this model are in the data folder under competition_benchmark. 

### Competition test results
The Zairachem-trained model provides both a binary classification score (0: inactive, 1: active) with a threshold of 2.5 uM and a prediction of the IC50 value itself:
* The classification model was able to predict correctly 30 out of the 33 molecules in the list
* The regression model predicted values of < 2.5 uM to 11 of the 12 real actives and > 2.5 to all real inactives

In addition, we trained a second model using a more restrictive cut-off of 1 uM for potency. Comparison of the different model performances can be found under data > competition_benchmark.

We subsequently retrained the pipeline with all available data (original training set + competition molecules + newest synthesized molecules), producing two models (with cut-offs for binary classification set at 1 and 2.5 uM respectively). Models can be downloaded ([1uM](https://zairachem-models.s3.eu-central-1.amazonaws.com/osm/osm_1uM_all.zip) and [2.5uM](https://zairachem-models.s3.eu-central-1.amazonaws.com/osm/osm_25uM_all.zip) cut-offs), and run with the [ZairaChem package](https://github.com/ersilia-os/zaira-chem)

## New generation of candidates based on high-actives
Using the methodology described by the [ETH Modlab](https://github.com/ETHmodlab/virtual_libraries) for low data generative models, we generated 683 new series 4 molecules using for transfer learning the best experimentally validated molecules (IC50 <= 1) (89 molecules) and the best molecules from Round 2 (90 molecules)

## Selection of highly potent candidates
We use the Zairachem model to select the highest active molecules (predicted active by both models as described in the [notebooks](https://github.com/ersilia-os/osm-series4-synthesis-round1/tree/main/notebooks)) from:
* Set of pre-selected candidates in round 2 (17.876 molecules): 1094 molecules
* New synthesis round based on high actives (683 molecules): 201 molecules
* Best compounds selected in round 2 (90 molecules): 35 molecules

We therefore provide the list of [35 candidates](https://github.com/ersilia-os/osm-series4-synthesis-round1/blob/main/data/high_actives_selection.csv) for experimental testing and an additional pool of [1295 molecules](https://github.com/ersilia-os/osm-series4-synthesis-round1/blob/main/data/high_actives_all.csv) which can be screened for interesting molecules as well.

These .csv files contain the smiles, the probability of being active with cut-off at 1uM and cut-of at 2.5uM, respectively, and the predicted IC50 using the regression model.
