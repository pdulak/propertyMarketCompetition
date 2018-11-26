# Machine Learning - Property competition

This Git repository contains the final notebook for my best score in Kaggle on [Data Workshop's](http://dataworkshop.eu/) [Property Market Forecast competition](https://www.kaggle.com/c/dataworskhopproperty), along with external data I used and few additional notebooks.

1) FINAL.ipynb - contains the best scoring solution.
2) "externalData" directory contains two CSV files with an external data used.
3) "final notebooks" directory contains set of useful notebooks you may want to review.

In this competition I used categorization functions by [Sławomir Zagórski](https://github.com/SlawomirZagorski/MachineLearning) and adjusted them to fit my needs.

### Additional notebooks information
In the "final notebooks" directory you will find the following notebooks:
* FINAL.ipynb - contains the best scoring solution.
* FINAL smaller amount of estimators.ipynb - contains the same solution with the smaller amount of estimators on each XGB model, this one is working faster and was used for tests on my new ideas
* FINAL with explanations.ipynb - the same solution with explanations in English
* FINAL z objasnieniami.ipynb - the same solution with explanations in Polish
* FINAL without prices from text.ipynb - the same solution without the feature generated from the text field
* Full_CV.ipynb - notebook to generate Cross Validation results on my full model stack

### Competition milestones
During the competition there were a few milestones I want to note:
* The first submissions to Kaggle were build using the default settings for **RandomForestRegressor and XGBRegressor**. **No additional features generated**, just a test. They scored **130894.57592** for RF and **130962.65716** for XGB
* Once I generated **four levels of localization, based on the 'localization' field**, my XGB result reached **81998.12736**
* After **proper preparation and categorization of all simple features** (without text and stats), XGB reached **72849.27242**
* In the meantime I performed some feature adjustments - cleanup of the outliers, review and generation of log from some of them, I saw no advantage of these changes. I also **added features related to the price per meter in the given localization** based on train data. This was havily used later.
* After the fist **HyperOpt** test, XGB reached **65461.91417** - this was generated to check how HyperOpt can change the results. With the same features, **Random Forest with max_depth=50, n_estimators=70** reached **61049.30362**
* Once I added features generated from stats and text field, the models reached: **61723.11447 for XGB, and 60161.05975 for Random Forest**
* I was trying **HyperOpt** again, received **havily overfitted model** (in my opinion) which scored **53272.39798**
* There was a **function added** to **modify predicted price using the data from the text field** (sometimes the price is written there) with the limit of change set to 200.000. This gives XGB the score of **51510.90506**
* Using **HyperOpt** I found second model with the good local score and the **predictions rather different from my first model**. This second XGB model scored **50893.53177**. Local MAE between models was about 10.000
* Using **blending** between my two models (50% for each) I reached **50490.92865**
* Using **stacking** with the third model (first two models generated the data used by the third model along with the data from feature engineering), I reached **50179.19565**
* I noticed that I was sending results to Kaggle based on the model training on **80% of the data**. Once I switched to the **full set** (whole training set), I reached **49752.58864**
* As the last significant step I removed the noise I intentionally added to the data before, this gave me the score of **47450.20984**
