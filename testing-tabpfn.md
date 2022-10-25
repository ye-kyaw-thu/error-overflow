# Testing with TabPFN

## Create a New Conda Environment

```
conda create --name tabPFN python=3.7
...
...
...
Downloading and Extracting Packages
pip-22.2.2           | 2.3 MB    | ######################################### | 100% 
zlib-1.2.13          | 103 KB    | ######################################### | 100% 
python-3.7.13        | 40.7 MB   | ######################################### | 100% 
setuptools-63.4.1    | 1.1 MB    | ######################################### | 100% 
readline-8.2         | 357 KB    | ######################################### | 100% 
certifi-2022.9.24    | 154 KB    | ######################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate tabPFN
#
# To deactivate an active environment, use
#
#     $ conda deactivate

Retrieving notices: ...working... done
```

## Entering into the New Environment

conda activate tabPFN

## Install TabPFN

(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ pip install tabpfn
Collecting tabpfn
  Downloading tabpfn-0.1.3-py3-none-any.whl (136 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 136.1/136.1 kB 1.7 MB/s eta 0:00:00
Collecting configspace>=0.4.21
  Downloading ConfigSpace-0.6.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.9/4.9 MB 3.0 MB/s eta 0:00:00
Collecting seaborn>=0.11.2
  Downloading seaborn-0.12.1-py3-none-any.whl (288 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 288.2/288.2 kB 3.7 MB/s eta 0:00:00
Collecting openml>=0.12.2
  Downloading openml-0.12.2.tar.gz (119 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 119.9/119.9 kB 9.2 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting hyperopt>=0.2.5
  Downloading hyperopt-0.2.7-py2.py3-none-any.whl (1.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 5.9 MB/s eta 0:00:00
Collecting torch>=1.9.0
  Downloading torch-1.12.1-cp37-cp37m-manylinux1_x86_64.whl (776.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 776.3/776.3 MB 1.0 MB/s eta 0:00:00
Collecting numpy>=1.21.2
  Using cached numpy-1.21.6-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (15.7 MB)
Collecting scikit-learn>=0.24.2
  Downloading scikit_learn-1.0.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (24.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24.8/24.8 MB 2.5 MB/s eta 0:00:00
Collecting gpytorch>=1.5.0
  Downloading gpytorch-1.8.1-py2.py3-none-any.whl (361 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 361.8/361.8 kB 4.4 MB/s eta 0:00:00
Collecting pyyaml>=5.4.1
  Downloading PyYAML-6.0-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (596 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 596.3/596.3 kB 5.8 MB/s eta 0:00:00
Collecting tqdm>=4.62.1
  Using cached tqdm-4.64.1-py2.py3-none-any.whl (78 kB)
Collecting cython
  Downloading Cython-0.29.32-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.9/1.9 MB 4.8 MB/s eta 0:00:00
Collecting pyparsing
  Using cached pyparsing-3.0.9-py3-none-any.whl (98 kB)
Collecting scipy
  Using cached scipy-1.7.3-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (38.1 MB)
Collecting typing-extensions
  Using cached typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting networkx>=2.2
  Downloading networkx-2.6.3-py3-none-any.whl (1.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.9/1.9 MB 4.9 MB/s eta 0:00:00
Collecting py4j
  Downloading py4j-0.10.9.7-py2.py3-none-any.whl (200 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 200.5/200.5 kB 3.5 MB/s eta 0:00:00
Collecting future
  Using cached future-0.18.2-py3-none-any.whl
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting cloudpickle
  Downloading cloudpickle-2.2.0-py3-none-any.whl (25 kB)
Collecting liac-arff>=2.4.0
  Downloading liac-arff-2.5.0.tar.gz (13 kB)
  Preparing metadata (setup.py) ... done
Collecting xmltodict
  Downloading xmltodict-0.13.0-py2.py3-none-any.whl (10.0 kB)
Collecting requests
  Using cached requests-2.28.1-py3-none-any.whl (62 kB)
Collecting python-dateutil
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pandas>=1.0.0
  Downloading pandas-1.3.5-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.3/11.3 MB 2.6 MB/s eta 0:00:00
Collecting minio
  Downloading minio-7.1.12-py3-none-any.whl (76 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 76.2/76.2 kB 1.8 MB/s eta 0:00:00
Collecting pyarrow
  Downloading pyarrow-9.0.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (35.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 35.3/35.3 MB 2.5 MB/s eta 0:00:00
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting joblib>=0.11
  Using cached joblib-1.2.0-py3-none-any.whl (297 kB)
Collecting matplotlib!=3.6.1,>=3.1
  Downloading matplotlib-3.5.3-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (11.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.2/11.2 MB 2.7 MB/s eta 0:00:00
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.4-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 4.8 MB/s eta 0:00:00
Collecting fonttools>=4.22.0
  Downloading fonttools-4.38.0-py3-none-any.whl (965 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 965.4/965.4 kB 4.6 MB/s eta 0:00:00
Collecting packaging>=20.0
  Using cached packaging-21.3-py3-none-any.whl (40 kB)
Collecting pillow>=6.2.0
  Downloading Pillow-9.2.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.1/3.1 MB 3.6 MB/s eta 0:00:00
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pytz>=2017.3
  Downloading pytz-2022.5-py2.py3-none-any.whl (500 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 500.7/500.7 kB 3.9 MB/s eta 0:00:00
Requirement already satisfied: certifi in /home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages (from minio->openml>=0.12.2->tabpfn) (2022.9.24)
Collecting urllib3
  Using cached urllib3-1.26.12-py2.py3-none-any.whl (140 kB)
Collecting charset-normalizer<3,>=2
  Using cached charset_normalizer-2.1.1-py3-none-any.whl (39 kB)
Collecting idna<4,>=2.5
  Using cached idna-3.4-py3-none-any.whl (61 kB)
Building wheels for collected packages: openml, liac-arff
  Building wheel for openml (setup.py) ... done
  Created wheel for openml: filename=openml-0.12.2-py3-none-any.whl size=137310 sha256=6ae472b3c822b049900d8ddf8d892f664fa68dda0dc874e3d19c31b9a19a0348
  Stored in directory: /home/ye/.cache/pip/wheels/6a/20/88/cf4ac86aa18e2cd647ed16ebe274a5dacee9d0075fa02af250
  Building wheel for liac-arff (setup.py) ... done
  Created wheel for liac-arff: filename=liac_arff-2.5.0-py3-none-any.whl size=11716 sha256=2d852ef410d28cf1c943ae78408f94625e45ce7bfe97be04100d73f3aadaccb2
  Stored in directory: /home/ye/.cache/pip/wheels/1f/0f/15/332ca86cbebf25ddf98518caaf887945fbe1712b97a0f2493b
Successfully built openml liac-arff
Installing collected packages: pytz, py4j, xmltodict, urllib3, typing-extensions, tqdm, threadpoolctl, six, pyyaml, pyparsing, pillow, numpy, networkx, liac-arff, joblib, idna, future, fonttools, cython, cycler, cloudpickle, charset-normalizer, torch, scipy, requests, python-dateutil, pyarrow, packaging, minio, kiwisolver, scikit-learn, pandas, matplotlib, hyperopt, configspace, seaborn, openml, gpytorch, tabpfn
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
nltk 3.5 requires click, which is not installed.
mchmm 0.4.1 requires graphviz, which is not installed.
Successfully installed charset-normalizer-2.1.1 cloudpickle-2.2.0 configspace-0.6.0 cycler-0.11.0 cython-0.29.32 fonttools-4.38.0 future-0.18.2 gpytorch-1.8.1 hyperopt-0.2.7 idna-3.4 joblib-1.2.0 kiwisolver-1.4.4 liac-arff-2.5.0 matplotlib-3.5.3 minio-7.1.12 networkx-2.6.3 numpy-1.21.6 openml-0.12.2 packaging-21.3 pandas-1.3.5 pillow-9.2.0 py4j-0.10.9.7 pyarrow-9.0.0 pyparsing-3.0.9 python-dateutil-2.8.2 pytz-2022.5 pyyaml-6.0 requests-2.28.1 scikit-learn-1.0.2 scipy-1.7.3 seaborn-0.12.1 six-1.16.0 tabpfn-0.1.3 threadpoolctl-3.1.0 torch-1.12.1 tqdm-4.64.1 typing-extensions-4.4.0 urllib3-1.26.12 xmltodict-0.13.0
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ 
```

## Install Two More Libraries 

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ pip install graphviz
Collecting graphviz
  Using cached graphviz-0.20.1-py3-none-any.whl (47 kB)
Installing collected packages: graphviz
Successfully installed graphviz-0.20.1
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ 
```

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ pip install click
Collecting click
  Using cached click-8.1.3-py3-none-any.whl (96 kB)
Collecting importlib-metadata
  Downloading importlib_metadata-5.0.0-py3-none-any.whl (21 kB)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages (from importlib-metadata->click) (4.4.0)
Collecting zipp>=0.5
  Downloading zipp-3.10.0-py3-none-any.whl (6.2 kB)
Installing collected packages: zipp, importlib-metadata, click
Successfully installed click-8.1.3 importlib-metadata-5.0.0 zipp-3.10.0
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ 
```

## Test-Run on CPU

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/tabpfn$ time python ./test-tabpfn1.py 
We have to download the TabPFN, as there is no checkpoint at  /home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/models_diff/prior_diff_real_checkpoint_n_0_epoch_100.cpkt
It has about 100MB, so this might take a moment.
Loading models_diff/prior_diff_real_checkpoint_n_0_epoch_100.cpkt
Loading....
Using style prior: True
MODEL BUILDER <module 'tabpfn.priors.differentiable_prior' from '/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/priors/differentiable_prior.py'> <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f7078c83290>
Using cpu:0 device
init dist
Not using distributed
DataLoader.__dict__ {'num_steps': 8192, 'get_batch_kwargs': {'batch_size': 1, 'eval_pos_seq_len_sampler': <function train.<locals>.eval_pos_seq_len_sampler at 0x7f7078c83950>, 'seq_len_maximum': 10, 'device': 'cpu:0', 'num_features': 100, 'hyperparameters': {'lr': 0.0001, 'dropout': 0.0, 'emsize': 512, 'batch_size': 1, 'nlayers': 12, 'num_features': 100, 'nhead': 4, 'nhid_factor': 2, 'bptt': 10, 'eval_positions': [972], 'seq_len_used': 50, 'sampling': 'mixed', 'epochs': 400, 'num_steps': 8192, 'verbose': False, 'mix_activations': True, 'nan_prob_unknown_reason_reason_prior': 1.0, 'categorical_feature_p': 0.2, 'nan_prob_no_reason': 0.0, 'nan_prob_unknown_reason': 0.0, 'nan_prob_a_reason': 0.0, 'max_num_classes': 10, 'num_classes': 2, 'noise_type': 'Gaussian', 'balanced': False, 'normalize_to_ranking': False, 'set_value_to_nan': 0.1, 'normalize_by_used_features': True, 'num_features_used': <function load_model.<locals>.<lambda> at 0x7f7078cf2cb0>, 'num_categorical_features_sampler_a': -1.0, 'differentiable_hyperparameters': {'distribution': 'uniform', 'min': 1000000.0, 'max': 1000001.0}, 'prior_type': 'prior_bag', 'differentiable': True, 'flexible': True, 'aggregate_k_gradients': 8, 'recompute_attn': True, 'bptt_extra_samples': None, 'dynamic_batch_size': False, 'multiclass_loss_type': 'nono', 'output_multiclass_ordered_p': 0.0, 'normalize_with_sqrt': False, 'new_mlp_per_example': True, 'prior_mlp_scale_weights_sqrt': True, 'batch_size_per_gp_sample': None, 'normalize_ignore_label_too': True, 'differentiable_hps_as_style': False, 'max_eval_pos': 1000, 'random_feature_rotation': True, 'rotate_normalized_labels': True, 'canonical_y_encoder': False, 'total_available_time_in_s': None, 'train_mixed_precision': True, 'efficient_eval_masking': True, 'multiclass_type': 'rank', 'done_part_in_training': 0.8425, 'categorical_features_sampler': <function load_model.<locals>.<lambda> at 0x7f70e17c2cb0>, 'num_features_used_in_training': '<function <lambda>.<locals>.<lambda> at 0x7fc575dfb5e0>', 'num_classes_in_training': '<function <lambda>.<locals>.<lambda> at 0x7fc575dfb550>', 'batch_size_in_training': 8, 'bptt_in_training': 1024, 'bptt_extra_samples_in_training': None, 'prior_bag_get_batch': (<function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f7078c83170>, <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f7078c83200>), 'prior_bag_exp_weights_1': 2.0, 'normalize_labels': True, 'check_is_compatible': True}, 'batch_size_per_gp_sample': None, 'get_batch': <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f7078c83290>, 'differentiable_hyperparameters': {'prior_bag_exp_weights_1': {'distribution': 'uniform', 'min': 1000000.0, 'max': 1000001.0}, 'num_layers': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 6, 'min_mean': 1, 'round': True, 'lower_bound': 2}, 'prior_mlp_hidden_dim': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 130, 'min_mean': 5, 'round': True, 'lower_bound': 4}, 'prior_mlp_dropout_prob': {'distribution': 'meta_beta', 'scale': 0.9, 'min': 0.1, 'max': 5.0}, 'noise_std': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 0.3, 'min_mean': 0.0001, 'round': False, 'lower_bound': 0.0}, 'init_std': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 0.01, 'round': False, 'lower_bound': 0.0}, 'num_causes': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 12, 'min_mean': 1, 'round': True, 'lower_bound': 1}, 'is_causal': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'pre_sample_weights': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'y_is_effect': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'prior_mlp_activations': {'distribution': 'meta_choice_mixed', 'choice_values': [<class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>], 'choice_values_used': ["<class 'torch.nn.modules.activation.Tanh'>", "<class 'torch.nn.modules.linear.Identity'>", '<function get_diff_causal.<locals>.<lambda> at 0x7fc575dfb670>', "<class 'torch.nn.modules.activation.ELU'>"]}, 'block_wise_dropout': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sort_features': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/amp/autocast_mode.py:198: UserWarning: User provided device_type of 'cuda', but CUDA is not available. Disabling
  warnings.warn('User provided device_type of \'cuda\', but CUDA is not available. Disabling')
/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/amp/autocast_mode.py:198: UserWarning: User provided device_type of 'cuda', but CUDA is not available. Disabling
  warnings.warn('User provided device_type of \'cuda\', but CUDA is not available. Disabling')
Accuracy 0.9840425531914894

real	1m1.497s
user	0m41.043s
sys	0m3.628s
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/tabpfn$
```

It's Work!!!  
  
## Testing with Our Data
  
Currently, our data that I used for SGD have only two columns. I plan to add keyword and thus made dummy three column (just copy col1 to col2) and made test run on CPU.  
  
```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/tabpfn$ python ./khpolar-tabpfn1.py 
training data format is as follows: 
                                                  text1  ...     label
8511  ▁ស ភាព ការ ណ៍ នេះ បាន ធ្វើឲ្យ ប្រ ជា ជន ស ប្ប ...  ...  positive
4621  ▁ព ាន រ ង ្វ ាន់ ▁ធ នា គ ារ ក្នុង ស្រ ុក ឆ្ ន ...  ...  positive
2236  ▁សូម អ ប អ រ សា ទ រ ទៅ ក ាន់ ក្រ ុ ម ជ ័យ ល ា ...  ...  positive
6915  ▁ក្រោយ ពេល កើត ហេតុ ▁សម ត្ថ កិច្ច ជ ំ ន ាញ ▁បា...  ...  positive
5658  ▁ចំពោះ ▁សណ្ឋាគា រ ▁ MH R ▁ការ ជ ួ យ ▁គឺជា ▁ក ា...  ...  positive

[5 rows x 3 columns]
Check after encoding ...
   text1  text2     label
0   7819   7819  positive
1   7961   7961  negative
2   5913   5913  positive
3   5651   5651  positive
4   9935   9935   neutral
Loading models_diff/prior_diff_real_checkpoint_n_0_epoch_100.cpkt
Loading....
Using style prior: True
MODEL BUILDER <module 'tabpfn.priors.differentiable_prior' from '/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/priors/differentiable_prior.py'> <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6d3272a7a0>
Using cpu:0 device
init dist
Not using distributed
DataLoader.__dict__ {'num_steps': 8192, 'get_batch_kwargs': {'batch_size': 1, 'eval_pos_seq_len_sampler': <function train.<locals>.eval_pos_seq_len_sampler at 0x7f6d3272ae60>, 'seq_len_maximum': 10, 'device': 'cpu:0', 'num_features': 100, 'hyperparameters': {'lr': 0.0001, 'dropout': 0.0, 'emsize': 512, 'batch_size': 1, 'nlayers': 12, 'num_features': 100, 'nhead': 4, 'nhid_factor': 2, 'bptt': 10, 'eval_positions': [972], 'seq_len_used': 50, 'sampling': 'mixed', 'epochs': 400, 'num_steps': 8192, 'verbose': False, 'mix_activations': True, 'nan_prob_unknown_reason_reason_prior': 1.0, 'categorical_feature_p': 0.2, 'nan_prob_no_reason': 0.0, 'nan_prob_unknown_reason': 0.0, 'nan_prob_a_reason': 0.0, 'max_num_classes': 10, 'num_classes': 2, 'noise_type': 'Gaussian', 'balanced': False, 'normalize_to_ranking': False, 'set_value_to_nan': 0.1, 'normalize_by_used_features': True, 'num_features_used': <function load_model.<locals>.<lambda> at 0x7f6d32742dd0>, 'num_categorical_features_sampler_a': -1.0, 'differentiable_hyperparameters': {'distribution': 'uniform', 'min': 1000000.0, 'max': 1000001.0}, 'prior_type': 'prior_bag', 'differentiable': True, 'flexible': True, 'aggregate_k_gradients': 8, 'recompute_attn': True, 'bptt_extra_samples': None, 'dynamic_batch_size': False, 'multiclass_loss_type': 'nono', 'output_multiclass_ordered_p': 0.0, 'normalize_with_sqrt': False, 'new_mlp_per_example': True, 'prior_mlp_scale_weights_sqrt': True, 'batch_size_per_gp_sample': None, 'normalize_ignore_label_too': True, 'differentiable_hps_as_style': False, 'max_eval_pos': 1000, 'random_feature_rotation': True, 'rotate_normalized_labels': True, 'canonical_y_encoder': False, 'total_available_time_in_s': None, 'train_mixed_precision': True, 'efficient_eval_masking': True, 'multiclass_type': 'rank', 'done_part_in_training': 0.8425, 'categorical_features_sampler': <function load_model.<locals>.<lambda> at 0x7f6d32742e60>, 'num_features_used_in_training': '<function <lambda>.<locals>.<lambda> at 0x7fc575dfb5e0>', 'num_classes_in_training': '<function <lambda>.<locals>.<lambda> at 0x7fc575dfb550>', 'batch_size_in_training': 8, 'bptt_in_training': 1024, 'bptt_extra_samples_in_training': None, 'prior_bag_get_batch': (<function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6d3272a680>, <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6d3272a710>), 'prior_bag_exp_weights_1': 2.0, 'normalize_labels': True, 'check_is_compatible': True}, 'batch_size_per_gp_sample': None, 'get_batch': <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6d3272a7a0>, 'differentiable_hyperparameters': {'prior_bag_exp_weights_1': {'distribution': 'uniform', 'min': 1000000.0, 'max': 1000001.0}, 'num_layers': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 6, 'min_mean': 1, 'round': True, 'lower_bound': 2}, 'prior_mlp_hidden_dim': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 130, 'min_mean': 5, 'round': True, 'lower_bound': 4}, 'prior_mlp_dropout_prob': {'distribution': 'meta_beta', 'scale': 0.9, 'min': 0.1, 'max': 5.0}, 'noise_std': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 0.3, 'min_mean': 0.0001, 'round': False, 'lower_bound': 0.0}, 'init_std': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 0.01, 'round': False, 'lower_bound': 0.0}, 'num_causes': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 12, 'min_mean': 1, 'round': True, 'lower_bound': 1}, 'is_causal': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'pre_sample_weights': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'y_is_effect': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'prior_mlp_activations': {'distribution': 'meta_choice_mixed', 'choice_values': [<class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>], 'choice_values_used': ["<class 'torch.nn.modules.activation.Tanh'>", "<class 'torch.nn.modules.linear.Identity'>", '<function get_diff_causal.<locals>.<lambda> at 0x7fc575dfb670>', "<class 'torch.nn.modules.activation.ELU'>"]}, 'block_wise_dropout': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sort_features': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/amp/autocast_mode.py:198: UserWarning: User provided device_type of 'cuda', but CUDA is not available. Disabling
  warnings.warn('User provided device_type of \'cuda\', but CUDA is not available. Disabling')
Traceback (most recent call last):
  File "./khpolar-tabpfn1.py", line 56, in <module>
    y_eval, p_eval = classifier.predict(X_test, return_winning_probability=True)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 210, in predict
    p = self.predict_proba(X, normalize_with_test=normalize_with_test)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 204, in predict_proba
    , **get_params_from_config(self.c))
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 439, in transformer_predict
    output_batch = checkpoint(predict, batch_input, batch_label, style_, softmax_temperature_, True)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/utils/checkpoint.py", line 235, in checkpoint
    return CheckpointFunction.apply(function, preserve, *args)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/utils/checkpoint.py", line 96, in forward
    outputs = run_function(*args)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 274, in predict
    single_eval_pos=eval_position)[:, :, 0:num_classes]
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/modules/module.py", line 1130, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/transformer.py", line 141, in forward
    output = self.transformer_encoder(src, src_mask)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/modules/module.py", line 1130, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/transformer.py", line 227, in forward
    output = mod(output, src_mask=mask, src_key_padding_mask=src_key_padding_mask)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/modules/module.py", line 1130, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/tabpfn/layer.py", line 109, in forward
    src_left = self.self_attn(src_[:single_eval_position], src_[:single_eval_position], src_[:single_eval_position])[0]
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/modules/module.py", line 1130, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/modules/activation.py", line 1160, in forward
    attn_mask=attn_mask, average_attn_weights=average_attn_weights)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/functional.py", line 5179, in multi_head_attention_forward
    attn_output, attn_output_weights = _scaled_dot_product_attention(q, k, v, attn_mask, dropout_p)
  File "/home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages/torch/nn/functional.py", line 4854, in _scaled_dot_product_attention
    attn = torch.bmm(q, k.transpose(-2, -1))
RuntimeError: [enforce fail at alloc_cpu.cpp:73] . DefaultCPUAllocator: can't allocate memory: you tried to allocate 15600421632 bytes. Error code 12 (Cannot allocate memory)
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/tabpfn$ python ./khpolar-tabpfn1.py 
```

I got above error! on CPU.

## Installation of TabPFN on Server  
  

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
