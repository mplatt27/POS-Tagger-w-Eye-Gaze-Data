# Semi-supervised PoS Tagger with Eye Gaze Data

This is a project completed as part of the course CS 6120 Natural Language Process at Northeastern Univesity. The goal is to explore improvements in semi-supervised tagging with eye gaze features. 

The main code for the study comes from Stratos and Collins (2015) "MINITAGGER", available at: https://github.com/karlstratos/minitagger and from the paper availbe at: https://www.aclweb.org/anthology/W15-1511.pdf

This study modifies the MINITAGGER code in order to accept eye gaze features, in addition to Brown cluster bitstrings. The word embedding features from Stratos and Collins (2015) are removed for this study. This study also adds a condition to run eye gaze and bitstring features together. 

----------
Input files:

1. Brown cluster bitstrings of the form

	[bitstring]		[word_type]		[frequency]

2. Eye gaze of the form

	[frequency] 	[word_type]		[feature_1 feature_2 ... feature_n]

3. (Partially) labeled data for all sequences (sequences seperated by a space)

	[word] [label]
	[word] [label]
	[word] [label]

	[word] [label]
	[word] [label]


----------
To obtain partially labeled datasets through active learning:

`python minitagger-modified.py train_path/train.txt --train --feature_template gaze --gaze_path path/gaze.txt --active --active_output_path tmp/active_output_file --active_seed_size 1 --active_step_size 1 --active_output_interval 1`

To train a model with partially (or fully) labeled datasets:

- With eye gaze features

`python minitagger-modified.py train_path/train.txt --model_path tmp/model_file --train --feature_template gaze --gaze_path path/gaze.txt`

- With bitstring features

`python minitagger-modified.py train_path/train.txt --model_path tmp/model_file --train --feature_template bitstrings --bitstring_path path/bigstrings.txt`

- With combination of eye gaze and bitstring features

`python minitagger-modified.py train_path/train.txt --model_path tmp/model_file --train --feature_template combo --bitstring_path path/bigstrings.txt --gaze_path path/gaze.txt`

	
To test hte model:

`python minitagger-modified.py train_path/train.txt --model_path tmp/model_file --prediction_path tmp/prediction_file`


----------
The eye gaze data comes from the GECO corpus (Cop et al. 2017)


----------
References:

Barrett, M., Bingel, J., Keller, F., & Søgaard, A. (2016). Weakly supervised part-of-speech tagging using eye-tracking data. Proceedings of the 54th Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers), 579–584.

Barrett, M., Gonzalez-Garduno, A. V., Frermann,L., & Søgaard, A. (2018). Unsupervised induction of   linguistic categories withrecords of reading, speaking, and writing. Proceedings of the 2018 Conference  of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1 (Long Papers), 2028–2038.

Barrett, M., Keller, F., & Søgaard, A. (2016). Cross-lingual transfer of correlations between parts of   speech and gaze features. Proceedings of COLING 2016, the 26th International Conference on Computational Linguistics: Technical Papers, 1330–1339.

Barrett, M., & Søgaard, A. (2015). Reading behavior predicts syntactic categories. CoNLL. 


Brown, P. F., Della Pietra, V. J., deSouza, P. V.,Lai, J. C., & Mercer, R. L. (1992). Class based n-gram models of natural language. Computational Linguistics,18(4), 467–480.


Cop, U., Dirix, N., Drieghe, D., & Duyck, W.(2017). Presenting geco: An eyetracking corpus of monolingual and bilingual sentence reading. Behavior Research Methods, 49, 602–615.

Fan, R.E., Chang, K.W., Hsieh, C.J., Wang,X.R., & Lin, C.J. (2008). Liblinear: A library for large linear classification. Journal of machine learning research, 9 (Aug), 1871–1874.

Hollenstein, N., Barrett, M., & Beinborn, L.(2020). Towards best practices for leveraging human language processing signals for natural language processing. Proceedings of the Second Workshop on Linguistic and Neurocognitive Resources, 15–27.

Liang, P. (2005). Semi-supervised learning for natural language. Masters thesis.

Stratos, K., & Collins, M. (2015). Simple semi-supervised POS tagging. Proceedings of the 1st Workshop on Vector Space Modeling for Natural Language Processing, 79–87.



