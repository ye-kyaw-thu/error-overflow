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

```
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
  
Preparing a new enviroment and installation of tabpfn on server ...  
  
```
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
python-3.7.13        | 40.7 MB   | ########################################################## | 100% 
setuptools-63.4.1    | 1.1 MB    | ########################################################## | 100% 
zlib-1.2.13          | 103 KB    | ########################################################## | 100% 
readline-8.2         | 357 KB    | ########################################################## | 100% 
certifi-2022.9.24    | 154 KB    | ########################################################## | 100% 
pip-22.2.2           | 2.3 MB    | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate tabpfn
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~$ conda activate tabpfn
```

```
(tabpfn) yekyaw.thu@gpu:~$ pip install tabpfn
Collecting tabpfn
  Downloading tabpfn-0.1.3-py3-none-any.whl (136 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 136.1/136.1 kB 623.7 kB/s eta 0:00:00
Collecting numpy>=1.21.2
  Downloading numpy-1.21.6-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (15.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 15.7/15.7 MB 29.6 MB/s eta 0:00:00
Collecting scikit-learn>=0.24.2
  Downloading scikit_learn-1.0.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (24.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24.8/24.8 MB 27.6 MB/s eta 0:00:00
Collecting hyperopt>=0.2.5
  Downloading hyperopt-0.2.7-py2.py3-none-any.whl (1.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 53.5 MB/s eta 0:00:00
Collecting gpytorch>=1.5.0
  Downloading gpytorch-1.8.1-py2.py3-none-any.whl (361 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 361.8/361.8 kB 64.4 MB/s eta 0:00:00
Collecting seaborn>=0.11.2
  Downloading seaborn-0.12.1-py3-none-any.whl (288 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 288.2/288.2 kB 56.3 MB/s eta 0:00:00
Collecting torch>=1.9.0
  Downloading torch-1.12.1-cp37-cp37m-manylinux1_x86_64.whl (776.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 776.3/776.3 MB 4.8 MB/s eta 0:00:00
Collecting openml>=0.12.2
  Downloading openml-0.12.2.tar.gz (119 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 119.9/119.9 kB 34.4 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting configspace>=0.4.21
  Downloading ConfigSpace-0.6.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.9/4.9 MB 23.6 MB/s eta 0:00:00
Collecting tqdm>=4.62.1
  Downloading tqdm-4.64.1-py2.py3-none-any.whl (78 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.5/78.5 kB 24.8 MB/s eta 0:00:00
Collecting pyyaml>=5.4.1
  Downloading PyYAML-6.0-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (596 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 596.3/596.3 kB 30.7 MB/s eta 0:00:00
Collecting pyparsing
  Downloading pyparsing-3.0.9-py3-none-any.whl (98 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.3/98.3 kB 25.8 MB/s eta 0:00:00
Collecting scipy
  Downloading scipy-1.7.3-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (38.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 38.1/38.1 MB 20.2 MB/s eta 0:00:00
Collecting cython
  Downloading Cython-0.29.32-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.9/1.9 MB 29.9 MB/s eta 0:00:00
Collecting typing-extensions
  Downloading typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting cloudpickle
  Downloading cloudpickle-2.2.0-py3-none-any.whl (25 kB)
Collecting six
  Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting future
  Downloading future-0.18.2.tar.gz (829 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 829.2/829.2 kB 30.2 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting py4j
  Downloading py4j-0.10.9.7-py2.py3-none-any.whl (200 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 200.5/200.5 kB 27.2 MB/s eta 0:00:00
Collecting networkx>=2.2
  Downloading networkx-2.6.3-py3-none-any.whl (1.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.9/1.9 MB 29.9 MB/s eta 0:00:00
Collecting liac-arff>=2.4.0
  Downloading liac-arff-2.5.0.tar.gz (13 kB)
  Preparing metadata (setup.py) ... done
Collecting xmltodict
  Downloading xmltodict-0.13.0-py2.py3-none-any.whl (10.0 kB)
Collecting requests
  Downloading requests-2.28.1-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.8/62.8 kB 16.3 MB/s eta 0:00:00
Collecting python-dateutil
  Downloading python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 247.7/247.7 kB 36.8 MB/s eta 0:00:00
Collecting pandas>=1.0.0
  Downloading pandas-1.3.5-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.3/11.3 MB 24.1 MB/s eta 0:00:00
Collecting minio
  Downloading minio-7.1.12-py3-none-any.whl (76 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 76.2/76.2 kB 23.2 MB/s eta 0:00:00
Collecting pyarrow
  Downloading pyarrow-9.0.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (35.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 35.3/35.3 MB 22.8 MB/s eta 0:00:00
Collecting joblib>=0.11
  Downloading joblib-1.2.0-py3-none-any.whl (297 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 298.0/298.0 kB 29.6 MB/s eta 0:00:00
Collecting threadpoolctl>=2.0.0
  Downloading threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting matplotlib!=3.6.1,>=3.1
  Downloading matplotlib-3.5.3-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (11.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.2/11.2 MB 24.5 MB/s eta 0:00:00
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.4-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 28.8 MB/s eta 0:00:00
Collecting packaging>=20.0
  Downloading packaging-21.3-py3-none-any.whl (40 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.8/40.8 kB 10.5 MB/s eta 0:00:00
Collecting fonttools>=4.22.0
  Downloading fonttools-4.38.0-py3-none-any.whl (965 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 965.4/965.4 kB 32.6 MB/s eta 0:00:00
Collecting cycler>=0.10
  Downloading cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pillow>=6.2.0
  Downloading Pillow-9.2.0-cp37-cp37m-manylinux_2_28_x86_64.whl (3.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.2/3.2 MB 27.5 MB/s eta 0:00:00
Collecting pytz>=2017.3
  Downloading pytz-2022.5-py2.py3-none-any.whl (500 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 500.7/500.7 kB 37.6 MB/s eta 0:00:00
Collecting urllib3
  Downloading urllib3-1.26.12-py2.py3-none-any.whl (140 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 140.4/140.4 kB 21.9 MB/s eta 0:00:00
Requirement already satisfied: certifi in ./.conda/envs/tabpfn/lib/python3.7/site-packages (from minio->openml>=0.12.2->tabpfn) (2022.9.24)
Collecting charset-normalizer<3,>=2
  Downloading charset_normalizer-2.1.1-py3-none-any.whl (39 kB)
Collecting idna<4,>=2.5
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.5/61.5 kB 20.3 MB/s eta 0:00:00
Building wheels for collected packages: openml, liac-arff, future
  Building wheel for openml (setup.py) ... done
  Created wheel for openml: filename=openml-0.12.2-py3-none-any.whl size=137310 sha256=643c0645a06a371778886bcfb2393a3357eb766533efbfe45c0f6b29bde88759
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/6a/20/88/cf4ac86aa18e2cd647ed16ebe274a5dacee9d0075fa02af250
  Building wheel for liac-arff (setup.py) ... done
  Created wheel for liac-arff: filename=liac_arff-2.5.0-py3-none-any.whl size=11716 sha256=2dac381cce9ff1b2755f6ad48176adbd4bc5d2451247571fb26fc72e16ec7348
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/1f/0f/15/332ca86cbebf25ddf98518caaf887945fbe1712b97a0f2493b
  Building wheel for future (setup.py) ... done
  Created wheel for future: filename=future-0.18.2-py3-none-any.whl size=491058 sha256=d7e9c4fb499a84ed8683e009c24882e9e80f653be83234fc50896c2d0353b71d
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/56/b0/fe/4410d17b32f1f0c3cf54cdfb2bc04d7b4b8f4ae377e2229ba0
Successfully built openml liac-arff future
Installing collected packages: pytz, py4j, xmltodict, urllib3, typing-extensions, tqdm, threadpoolctl, six, pyyaml, pyparsing, pillow, numpy, networkx, liac-arff, joblib, idna, future, fonttools, cython, cycler, cloudpickle, charset-normalizer, torch, scipy, requests, python-dateutil, pyarrow, packaging, minio, kiwisolver, scikit-learn, pandas, matplotlib, hyperopt, configspace, seaborn, openml, gpytorch, tabpfn
Successfully installed charset-normalizer-2.1.1 cloudpickle-2.2.0 configspace-0.6.0 cycler-0.11.0 cython-0.29.32 fonttools-4.38.0 future-0.18.2 gpytorch-1.8.1 hyperopt-0.2.7 idna-3.4 joblib-1.2.0 kiwisolver-1.4.4 liac-arff-2.5.0 matplotlib-3.5.3 minio-7.1.12 networkx-2.6.3 numpy-1.21.6 openml-0.12.2 packaging-21.3 pandas-1.3.5 pillow-9.2.0 py4j-0.10.9.7 pyarrow-9.0.0 pyparsing-3.0.9 python-dateutil-2.8.2 pytz-2022.5 pyyaml-6.0 requests-2.28.1 scikit-learn-1.0.2 scipy-1.7.3 seaborn-0.12.1 six-1.16.0 tabpfn-0.1.3 threadpoolctl-3.1.0 torch-1.12.1 tqdm-4.64.1 typing-extensions-4.4.0 urllib3-1.26.12 xmltodict-0.13.0
(tabpfn) yekyaw.thu@gpu:~$
```

Successfully installed!!!  
  
## Test run on Server
 
form the GitHub site, I took the example running python code of tabpfn and testing as follows:  
  
```
from sklearn.metrics import accuracy_score
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split

from tabpfn.scripts.transformer_prediction_interface import TabPFNClassifier

X, y = load_breast_cancer(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)

classifier = TabPFNClassifier(device='cpu')
classifier.fit(X_train, y_train)
y_eval, p_eval = classifier.predict(X_test, return_winning_probability=True)

print('Accuracy', accuracy_score(y_test, y_eval))
```

Test run on server ...  
  
```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ python ./test-tabpfn.py 
^CTraceback (most recent call last):
  File "./test-tabpfn.py", line 5, in <module>
    from tabpfn.scripts.transformer_prediction_interface import TabPFNClassifier
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 7, in <module>
    from tabpfn.utils import normalize_data, to_ranking_low_mem, remove_outliers
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/utils.py", line 124, in <module>
    default_device = 'cuda:0' if torch.cuda.is_available() else 'cpu:0'
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/torch/cuda/__init__.py", line 83, in is_available
    return torch._C._cuda_getDeviceCount() > 0
KeyboardInterrupt
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./test-tabpfn.py 
We have to download the TabPFN, as there is no checkpoint at  /home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/models_diff/prior_diff_real_checkpoint_n_0_epoch_100.cpkt
It has about 100MB, so this might take a moment.
Loading models_diff/prior_diff_real_checkpoint_n_0_epoch_100.cpkt
Loading....
Using style prior: True
MODEL BUILDER <module 'tabpfn.priors.differentiable_prior' from '/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/priors/differentiable_prior.py'> <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6160952cb0>
Using cpu device
init dist
Not using distributed
DataLoader.__dict__ {'num_steps': 8192, 'get_batch_kwargs': {'batch_size': 1, 'eval_pos_seq_len_sampler': <function train.<locals>.eval_pos_seq_len_sampler at 0x7f616096a3b0>, 'seq_len_maximum': 10, 'device': 'cpu', 'num_features': 100, 'hyperparameters': {'lr': 0.0001, 'dropout': 0.0, 'emsize': 512, 'batch_size': 1, 'nlayers': 12, 'num_features': 100, 'nhead': 4, 'nhid_factor': 2, 'bptt': 10, 'eval_positions': [972], 'seq_len_used': 50, 'sampling': 'mixed', 'epochs': 400, 'num_steps': 8192, 'verbose': False, 'mix_activations': True, 'nan_prob_unknown_reason_reason_prior': 1.0, 'categorical_feature_p': 0.2, 'nan_prob_no_reason': 0.0, 'nan_prob_unknown_reason': 0.0, 'nan_prob_a_reason': 0.0, 'max_num_classes': 10, 'num_classes': 2, 'noise_type': 'Gaussian', 'balanced': False, 'normalize_to_ranking': False, 'set_value_to_nan': 0.1, 'normalize_by_used_features': True, 'num_features_used': <function load_model.<locals>.<lambda> at 0x7f6161f06710>, 'num_categorical_features_sampler_a': -1.0, 'differentiable_hyperparameters': {'distribution': 'uniform', 'min': 1000000.0, 'max': 1000001.0}, 'prior_type': 'prior_bag', 'differentiable': True, 'flexible': True, 'aggregate_k_gradients': 8, 'recompute_attn': True, 'bptt_extra_samples': None, 'dynamic_batch_size': False, 'multiclass_loss_type': 'nono', 'output_multiclass_ordered_p': 0.0, 'normalize_with_sqrt': False, 'new_mlp_per_example': True, 'prior_mlp_scale_weights_sqrt': True, 'batch_size_per_gp_sample': None, 'normalize_ignore_label_too': True, 'differentiable_hps_as_style': False, 'max_eval_pos': 1000, 'random_feature_rotation': True, 'rotate_normalized_labels': True, 'canonical_y_encoder': False, 'total_available_time_in_s': None, 'train_mixed_precision': True, 'efficient_eval_masking': True, 'multiclass_type': 'rank', 'done_part_in_training': 0.8425, 'categorical_features_sampler': <function load_model.<locals>.<lambda> at 0x7f620638ecb0>, 'num_features_used_in_training': '<function <lambda>.<locals>.<lambda> at 0x7fc575dfb5e0>', 'num_classes_in_training': '<function <lambda>.<locals>.<lambda> at 0x7fc575dfb550>', 'batch_size_in_training': 8, 'bptt_in_training': 1024, 'bptt_extra_samples_in_training': None, 'prior_bag_get_batch': (<function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6160952b90>, <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6160952c20>), 'prior_bag_exp_weights_1': 2.0, 'normalize_labels': True, 'check_is_compatible': True}, 'batch_size_per_gp_sample': None, 'get_batch': <function get_model.<locals>.make_get_batch.<locals>.new_get_batch at 0x7f6160952cb0>, 'differentiable_hyperparameters': {'prior_bag_exp_weights_1': {'distribution': 'uniform', 'min': 1000000.0, 'max': 1000001.0}, 'num_layers': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 6, 'min_mean': 1, 'round': True, 'lower_bound': 2}, 'prior_mlp_hidden_dim': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 130, 'min_mean': 5, 'round': True, 'lower_bound': 4}, 'prior_mlp_dropout_prob': {'distribution': 'meta_beta', 'scale': 0.9, 'min': 0.1, 'max': 5.0}, 'noise_std': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 0.3, 'min_mean': 0.0001, 'round': False, 'lower_bound': 0.0}, 'init_std': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 0.01, 'round': False, 'lower_bound': 0.0}, 'num_causes': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 12, 'min_mean': 1, 'round': True, 'lower_bound': 1}, 'is_causal': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'pre_sample_weights': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'y_is_effect': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'prior_mlp_activations': {'distribution': 'meta_choice_mixed', 'choice_values': [<class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>, <class 'torch.nn.modules.activation.Tanh'>], 'choice_values_used': ["<class 'torch.nn.modules.activation.Tanh'>", "<class 'torch.nn.modules.linear.Identity'>", '<function get_diff_causal.<locals>.<lambda> at 0x7fc575dfb670>', "<class 'torch.nn.modules.activation.ELU'>"]}, 'block_wise_dropout': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sort_features': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
Accuracy 0.9840425531914894

real	0m21.072s
user	1m0.861s
sys	0m4.356s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ 
```

Testing finished successfully!
  
## Preparing for Running on Server

I copied data to server ... 

I hidden ip-address, port-no and path on purpose for the security reason:  

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/tabpfn$ scp -r -P xxxx -i /xxx/id_rsa * yekyaw.thu@xxx.xx.xx.xxx:/home/yekyaw.thu/exp/kh-polar
```

## 1st Time Running with Khmer Data on Server
  
```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn1.py
...
...
...
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Accuracy 0.583

real	1m27.571s
user	12m17.147s
sys	2m37.095s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$
```

I used only two columns and thus plan to add key-word for the next time training.  

## Training with GPU
  
Updated the code as follows:  
  
``` 
#classifier = TabPFNClassifier(device='cpu')
classifier = TabPFNClassifier(device='cuda')
```

When I run with CUDA, I got following errors:  
  
```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn1.py
...
...
...
     return forward_call(*input, **kwargs)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/torch/nn/modules/activation.py", line 1160, in forward
    attn_mask=attn_mask, average_attn_weights=average_attn_weights)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/torch/nn/functional.py", line 5179, in multi_head_attention_forward
    attn_output, attn_output_weights = _scaled_dot_product_attention(q, k, v, attn_mask, dropout_p)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/torch/nn/functional.py", line 4856, in _scaled_dot_product_attention
    attn = softmax(attn, dim=-1)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/torch/nn/functional.py", line 1834, in softmax
    ret = input.softmax(dim)
RuntimeError: CUDA out of memory. Tried to allocate 7.27 GiB (GPU 0; 10.76 GiB total capacity; 8.24 GiB already allocated; 1.53 GiB free; 8.27 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF

real	0m6.349s
user	0m3.574s
sys	0m3.142s 
```

## Three Column Preparation

Recheck, keyword, files: 

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ head test.key-word.combine.shuffle.csv 
ច្បាស់លាស់,positive
គួរឱ្យភ្ញាក់ផ្អើល,positive
ភាពស្មោះត្រង់,positive
យកឈ្នះលើឧបសគ្គ/ក្តីសង្ឃឹមនៃអនាគតរបស់មនុស្សជាតិ,positive
ការ​ទទួល​បាន​នូវ​​មូលនិធិ​សប្បុរសជន​,positive
វាកាន់តែធ្ងន់ធ្ងរឡើង,negative
ទង្វើប្រកបដោយភាពកក់ក្តៅ/ជំនឿចិត្ត/ក្តីអង់អាចក្លាហាន,positive
ការចាំបាច់​,positive
ជំរុញឱ្យមានការព្រមាន,negative
ចិត្ត​ជ្រះថ្លា,positive
```

for training side:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ head train.key-word.combine.csv 
ដឹងឮ​កាន់តែ​ខ្លាំង,positive
សហការ,positive
សហការជាមួយអាជ្ញាធរមានសមត្ថកិច្ច,positive
ម្តាយដ៏ល្អ,positive
ពេល​វេលា​បណ្តាល​ឲ្យ​ខ្ញុំ​បាន​ស្គាល់​មនុស្ស​ល្អ​,positive
ជួយ​ដោះស្រាយ​ជីវភាព​គ្រួសារ,positive
ចាត់ការ​បន្ត​តាម​នីតិវិធី​ច្បាប់,positive
រក្សាស្ថិរភាពបានជាធម្មតា/មិនបង្កបញ្ហាធ្ងន់ធ្ងរអ្វីឡើយ​​​,positive
ឱកាស​មាស/ការ​អភិវឌ្ឍ​ខ្លាំង​,positive
ដាក់​ទំនាយ​/ជួប​តែ​រឿង​អាក្រក់/​រស់នៅ​ដោយ​គ្មាន​សេចក្តីសុខ​,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ wc ./train.key-word.combine.csv 
  9014   9327 744276 ./train.key-word.combine.csv
```

Finding ...  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ head train.sentence.key-word.shuffle.csv 
កាត់បន្ថយហានិភ័យគ្រោះថ្នាក់,positive
ពិតជាពិបាកនឹងទទួលយកខ្លាំងណាស់,negative
វិធានការអន្តរាគមន៍ជំនួយសង្គម,positive
ពួកគេមើលឃើញខ្លួនឯងអន់ថយ,negative
ទទួលស្វាគមន៍,positive
ចុះជួយច្រូតស្រូវប្រជាពលរដ្ឋរងគ្រោះដោយទឹកជំនន់,positive
អ្នកស្រី​ពិត​ជារំភើប​មែន​ទែន​,positive
លះបង់ទាំងកម្លាំងកាយ​/ការមើលថែ,positive
វាប្រព្រឹត្តិទៅមិនដូចគ្នា,negative
ហត់ចិត្តអត់ទទួលការរិះគន់ទេ,negative
```

comparing with sentence:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ head train.sentence.combine.shuffle.csv 
លោកសង្កត់ធ្ងន់ថា៖ «ខ្លឹមសារនៃកិច្ចសន្យា បើកទូលាយដែរ ដោយយើងទទួលគាត់ជាគ្រូបង្វឹកទាំងបាល់ទះឆ្នេរខ្សាច់ក្តី បាល់ទះក្នុងសាលក្តី រយៈពេល១ឆ្នាំ បើងាកមើលទៅក្រោយស៊ីហ្គេម ឆ្នាំ២០២៣ ចប់រយៈ៣ខែ ទើបផុតកិច្ចសន្យា។,positive
លោក Manele បានលើកឡើងថា៖«នៅក្នុងកិច្ចព្រមព្រៀងនោះមានចំណុចមួយចំនួនដែលប៉ះពាល់ដល់កោះសូឡូម៉ុន​​​។,negative
ប៉ុន្តែក្រៅពីភាពបៃតងនៅអាចមានចំណុចផ្សេងទៀត ដែលសម្តេចក្រឡាហោម ស ខេង ថ្លែងថា បៃតងហ្នឹងជាចំណុចទាក់ទាញមួយ ប៉ុន្តែវានៅមានឥរិយាបថ អាកប្បកិរិយា ភាពទន់ភ្លន់រួសរាយរាក់ទាក់ សុភាពរាបសារ ការទាក់ទាញរបស់យើងជាម្ចាស់ផ្ទះផងដែរ។​,positive
បន្ទាប់ពីបាញ់បំបុករួច ថ្មីៗនេះ NASA បានប្រកាសពីជោគជ័យយ៉ាងធំធេងរបស់ខ្លួន ដោយអាចម៍ផ្កាយ Dimorphos បានហោះខុសគន្លង តាមបំណងប្រាថ្នាហើយ។​,positive
៣. ​មធ្យមសិក្សា​៖ ក្រសួង​បាន​ផលិត​ខ្សែ​វីដេអូ​បង្រៀន សម្រាប់​ថ្នាក់​ទី ៧ ដល់​១២ និង​បាន​ជំរុញ​ឱ្យ​សាលារៀន​ផ្តល់​លទ្ធភាព​ឱ្យ​សិស្ស​បាន​ខ្ចី​សៀវភៅ​សិក្សា​គោល ដើម្បី​ស្វ័យ​សិក្សា​បន្ថែម​រៀងៗ​ខ្លួន​។​​​,neutral
អ្ននកប្រើប្រាស់​បណ្តាញ​សង្គម​បញ្ចេញមតិ​ជុំវិញ​ភរិយា​លោកនាយក​រដ្ឋមន្តរី ហ៊ុន សែន សាងសង់​ចេតិយ​ទុក​ឲ្យ​ប្តី​រួចហើយ គឺ​ស្ថិត​នៅ​ក្នុង​វត្ត មុនីសុវណ្ណ ឬ​វត្ត​ចំពុះក្អែក ខណ្ឌ​ច្បារអំពៅ​រាជធានី​ភ្នំពេញ តែ​លោក​មិន​ទទួល​យក​ឡើយ។​,negative
ការទទួលបានគ្រឿងឥស្សរិយយសរបស់ឯកឧត្តមបណ្ឌិត ធ្វើឡើងក្នុងពិធីបើកមហា​សន្និបា​ត​ក្រុមប្រឹក្សាអូឡាំពិកអាស៊ី នៅថ្ងៃទី០៤ ខែតុលានេះ ក្រោមអធិបតីភាព​ដ៏ខ្ពង់​ខ្ពស់​របស់​ស​ម្តេចតេជោ ហ៊ុន សែន នាយករដ្ឋមន្តរីនៃកម្ពុជា​​​។,positive
ដូច្នេះ​ការ​ចាំ​ដល់​ពេល​ចាស់​បាន​សិក្សា​ពី​ធម៌​មែនទែន​ទៅ​វា​ហាក់ជា​ការ​ហួសពេល​ទៅ​ហើយ​។,negative
អ្វីដែលអ្នកអាចធ្វើនៅថ្ងៃនេះ ដើម្បីធានាថា ថ្ងៃស្អែកសុខភាពរបស់អ្នក នឹងល្អប្រសើរនោះ គឺការប្រយ័ត្នប្រយែងទៅនិងរបបអាហាររបស់អ្នក ។,positive
សេតវិមានបានលើកឡើងថា ខ្លួននឹងពិគ្រោះជាមួយសភាលើការផ្គត់ផ្គង់នេះបន្ថែម ដើម្បីកាត់បន្ថយការគ្រប់គ្រងរបស់ក្រុមជួញដូរលើតម្លៃថាមពលនៅក្នុងសេចក្តីយោងជាក់ស្តែងមួយចំពោះច្បាប់​​​។,neutral
```

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ head test.key-word.combine.shuffle.csv 
ច្បាស់លាស់,positive
គួរឱ្យភ្ញាក់ផ្អើល,positive
ភាពស្មោះត្រង់,positive
យកឈ្នះលើឧបសគ្គ/ក្តីសង្ឃឹមនៃអនាគតរបស់មនុស្សជាតិ,positive
ការ​ទទួល​បាន​នូវ​​មូលនិធិ​សប្បុរសជន​,positive
វាកាន់តែធ្ងន់ធ្ងរឡើង,negative
ទង្វើប្រកបដោយភាពកក់ក្តៅ/ជំនឿចិត្ត/ក្តីអង់អាចក្លាហាន,positive
ការចាំបាច់​,positive
ជំរុញឱ្យមានការព្រមាន,negative
ចិត្ត​ជ្រះថ្លា,positive
```

comparing with sentence:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ head test.sentence.combine.shuffle.csv 
ចំពោះរមណីដ្ឋានដែលភ្ញៀវទេសចរចូលចិត្តទៅច្រើនជាងគេនោះគឺ រមណីដ្ឋានឡូរីជើងភ្នំបាណន់៕,positive
អ្នកដឹង​ទេ​? ដោយសារតែ​កញ្ញា សេង ធារី មាន​ឆន្ទៈ និង​កម្លាំងកាយ​រឹងមាំ​នេះ​ហើយ ការណ៍​នេះ​បាន​ធ្វើ​កញ្ញា​អាច​យក​ឈ្នះ​ចំពោះ​ស្ថានភាព​អាក្រក់​បែបនេះ​ពី​មួយ​ថ្ងៃ​ទៅ​មួយ​ថ្ងៃ​បាន។​,positive
បើ​យោង​តាម​ការ​ចុះ​ផ្សាយ​របស់​អង្គការ​កសិករ​ពិភពលោក​ (WFO)​ អំឡុង​ពេល​នៃ​ជំងឺ​រាតត្បាត​កូ​វី​ដ​-១៩​ កសិករ​ក្រីក្រ​បាន​ជួបនឹង​បញ្ហា​ប្រឈម​ក្នុង​ការ​បែងចែក​ប្រាក់​ចំណូល​ដើម្បី​ទុក​ទិញ​ផលិតផល​សុខាភិបាល​ គួប​ផ្សំ​ជាមួយនឹង​ការ​ធ្លាក់​ចុះ​នូវ​វត្តមាន​របស់​ឈ្មួញកណ្តាល​ និង​កង្វះខាត​មធ្យោបាយ​ក្នុង​ការ​ដឹក​ជញ្ជូន​កសិផល​ទៅ​កាន់​ទីផ្សារ​។,positive
វាមានភាពប៉ះពាល់នេះខ្លាំង នៅពេលដែលយើងប្រើឧបករណ៍នៅជិតភ្នែក។,negative
គាត់ស្តាប់តែមនុស្សនិយាយក្នុងទូរស័ព្ទ ប៉ុន្តែគាត់មិនដែលស្តាប់រឿងដែលខ្ញុំចង់និយាយប្រាប់ពួកគាត់នោះទេ ដូច្នេះហើយទើបក្តីសុបិនរបស់ខ្ញុំ គឺខ្ញុំចង់ក្លាយជាទូរស័ព្ទ។,negative
ក្នុងន័យតែមួយគត់ គឺយើងចង់បានមេដាយមាស ពេលកម្ពុជាធ្វើជាម្ចាស់ផ្ទះ កីឡាស៊ីហ្គេម។,positive
ខ្ញុំខ្លាចធ្វើមិនបាន,negative
ក៏កាលនោះ មានភិក្ខុមួយអង្គធ្វើដំណើរពីវត្តជេតពន ទៅតាមលំដាប់ បានដល់កន្លែងដែលភិក្ខុកម្លោះនោះគង់នៅ ភិក្ខុកម្លោះនោះ ក៏​បាន​ធ្វើ​កិច្ច​វត្ត​ចំពោះ​លោក​ជា​អ្នក​មកដល់ថ្មី ឲ្យគង់ក្នុងទីស្រួល សមរម្យហើយក៏សួរថា៖,positive
ដោយ​ស្នាមញញឹម នាង Stone សារភាពថា​នាង​បាក់​ទឹកចិត្ត​។,negative
អរគុណដែលបានផ្គត់ផ្គង់អោយកូនរៀនបានចប់ មានការងារល្អ ប្តូរដោយញើសស្រក់ជាច្រើនដំណក់ក្នុងការធ្វើកាងាររកលុយមកផ្គត់ផ្គង់គ្រួសារ មិនដែលរអ៊ូថាហត់ឡើយ ថែរក្សាកូនតាំងពីចាប់កំណើត ដឹងក្តី រហូតដល់ពេញវ័យ តែងតែអោយអ្វីដែលកូនចង់បាន អប់រំទូន្មាន ប្រៀនប្រដៅអោយកូនធ្វើអំពើល្អ ស្មោះត្រង់ ប្រព្រឹត្តតែរឿងល្អៗ,positive
```

After checking above, I think I only shuffle the sentence side and thus, difficult to rematch and I will took before shuffle pairs ...  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ wc ./train.sentence.combine.csv 
   9014   55743 4407928 ./train.sentence.combine.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ head -n 5 ./train.key-word.combine.csv 
ដឹងឮ​កាន់តែ​ខ្លាំង,positive
សហការ,positive
សហការជាមួយអាជ្ញាធរមានសមត្ថកិច្ច,positive
ម្តាយដ៏ល្អ,positive
ពេល​វេលា​បណ្តាល​ឲ្យ​ខ្ញុំ​បាន​ស្គាល់​មនុស្ស​ល្អ​,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ head -n 5 ./train.sentence.combine.csv 
ការ​ឃុំខ្លួន​កញ្ញា សេង ធារី កាន់តែ​យូរ​ដោយ​រដ្ឋាភិបាល​លោក ហ៊ុន សែន នោះ​នឹង​ធ្វើ​ឱ្យ​មនុស្សម្នា​កាន់​តែ​ច្រើន​ដឹងឮ​កាន់តែ​ខ្លាំង​អំពី​របប​ផ្តាច់ការ​នេះ និង​ការណ៍​ដែល​របប​នេះ​ពុំ​មាន​ឆន្ទៈ​អនុញ្ញាត​ឱ្យ​មាន​សំឡេង​នយោបាយ​ប្រឆាំង ព្រមទាំង​វិធី​ដែល​លោក ហ៊ុន សែន រក្សា​អំណាច​ដោយ​ប្រើ​កណ្តាប់​ដៃ​ដែក​របស់​គាត់​។​,positive
សូមបញ្ជាក់ថា ក្រុមការងារក្រសួងមហាផ្ទៃបានសហការជាមួយអាជ្ញាធរខេត្តព្រះ សីហនុ បានចុះបង្ករាបទីតាំងល្បែងខុសច្បាប់ចំនួន៥ទីតាំង នៅក្នុងក្រុងព្រះសីហនុ និងបាន រកឃើញជនបរទេសចម្រុះជាតិសាសន៍៕,positive
ក្នុងលិខិតបានបញ្ជាក់ថា ក្រុមការងារបង្ករាបមានតួនាទីភារកិច្ចក្នុងការរៀបចំផែនការ វិធានការ គោលការណ៍ណែនាំ ដើម្បីឱ្យអាជ្ញាធរមានសមត្ថកិច្ចគ្រប់លំដាប់ថ្នាក់ អនុវត្តបង្ករាបនូវរាល់ការលេងល្បែងស៊ីសងខុសច្បាប់គ្រប់ប្រភេទ និងត្រូវសហការជាមួយអាជ្ញាធរមានសមត្ថកិច្ចទាំងនៅថ្នាក់ជាតិ រដ្ឋបាលថ្នាក់ក្រោមជាតិ ដើម្បីធ្វើការស្រាវជ្រាវ និងចាត់វិធានការបង្ករាបនូវទីតាំងលេងល្បែងស៊ីសងខុសច្បាប់។,positive
យុវនារីណាដែលកាន់សៀវភៅពេលបច្ចុប្បន្ន គឺនឹងក្លាយទៅជាម្តាយដ៏ល្អនាពេលអនាគត។,positive
-​ ខ្ញុំ​នៅតែ​នឹក​ នៅ​តែ​ស្រលាញ់​គេ​ ប៉ុន្តែ​ពេល​វេលា​បណ្តាល​ឲ្យ​ខ្ញុំ​បាន​ស្គាល់​មនុស្ស​ល្អ​ម្នាក់​ទៀត​ ដែល​ផ្តល់​រសជាតិ​ជីវិត​មួយ​បែប​ផ្សេង​..,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ 

```

Confirmation with tail part:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ tail -n 5 ./train.key-word.combine.csv 
ក្រាបទូល,neutral
ស៊ុតបញ្ចូលទី,neutral
សាងសង់,neutral
បញ្ចេញ,neutral
ក្រាបទូល,neutral
```

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv$ tail -n 5 ./train.sentence.combine.csv 
ចៅកាំបិតបន្ទោះដងមួយក្រាបទូលថា«ទូលព្រះបង្គំកាប់នឹងកាំបិតបន្ទោះដងមួយ»,neutral
Messi បានបង្ហាញខ្លួនឱ្យក្រុមជម្រើសជាតិ អាហ្សង់ទីន ចំនួន១៦៤ ប្រកួត និងស៊ុតបញ្ចូលទីបាន៩០គ្រាប់ ចាប់តាំងពីឆ្នាំ២០០៥ មកម្ល៉េះ​​​។,neutral
ទាំង​ភោជនីយដ្ឋាន និង​ណូរី​ ត្រូវបាន​សាងសង់​រួចហើយ​តាំងពី​ឆ្នាំ​ ២០២១ ដោយ​ផ្តើម​ទទួលភ្ញៀវ​ជា​ក្រុម​ឯកជន​សម្រាប់តែ​ការ​កក់​ទុក​មុន​។​​​,neutral
គ្រឿងអេឡិចត្រូនិករបស់យើង បញ្ចេញពន្លឺខៀវ។,neutral
ចោរនោះធ្វើពុំកើតក៏ក្រាបទូលថា“ខ្ញុំព្រះបាទអម្ចាស់បានពីប្រពន្ធ”,neutral

```

OK. Go to test data side:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ head -n 5 ./test.key-word.combine.csv 
សិក្សា​ស្វែង​យល់/អនុវត្ត​ផ្ទាល់​,positive
ល្អប្រសើរ/គាប់ចិត្ត,positive
 កសិករ​ក្រីក្រ​បាន​ជួបនឹង​បញ្ហា​ប្រឈម/កង្វះខាត​មធ្យោបាយ,positive
ប្រយុទ្ធនឹងបញ្ហាកង្វះអាហារូបត្ថម្ភ,positive
ស្រឡាញ់,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ head -n 5 ./test.sentence.combine.csv 
ប៉ុន្តែ​នៅ​ពេល​នេះ​មានការ​សង្កេត​ឃើញ​ថា យុវជន និង​មនុស្ស​វ័យ​កណ្តាល​ដ​ច្រើន បាន​នាំ​គ្នា​សិក្សា​ស្វែង​យល់​ពី​ធម៌​ព្រះពុទ្ធ​ដើម្បី​យក​មក​អនុវត្ត​ផ្ទាល់​នៅ​ក្នុង​ជីវិត​រស់​ប្រចាំ​ថ្ងៃ​។,positive
ចំពោះរឿងគ្រួសារ និងស្នេហា គឺល្អប្រសើរ គាប់ចិត្ត គាប់ភ្នែកអ្នកផង៕,positive
បើ​យោង​តាម​ការ​ចុះ​ផ្សាយ​របស់​អង្គការ​កសិករ​ពិភពលោក​ (WFO)​ អំឡុង​ពេល​នៃ​ជំងឺ​រាតត្បាត​កូ​វី​ដ​-១៩​ កសិករ​ក្រីក្រ​បាន​ជួបនឹង​បញ្ហា​ប្រឈម​ក្នុង​ការ​បែងចែក​ប្រាក់​ចំណូល​ដើម្បី​ទុក​ទិញ​ផលិតផល​សុខាភិបាល​ គួប​ផ្សំ​ជាមួយនឹង​ការ​ធ្លាក់​ចុះ​នូវ​វត្តមាន​របស់​ឈ្មួញកណ្តាល​ និង​កង្វះខាត​មធ្យោបាយ​ក្នុង​ការ​ដឹក​ជញ្ជូន​កសិផល​ទៅ​កាន់​ទីផ្សារ​។,positive
(រាជធានីភ្នំពេញ)៖ ភាគីពាក់ព័ន្ធ ដែលកំពុងធ្វើការយ៉ាងសកម្មលើការលើកកម្ពស់បញ្ហាអាហារូបត្ថម្ភនៅកម្ពុជា បានប្តេជ្ញារួមគ្នា ប្រយុទ្ធនឹងបញ្ហាកង្វះអាហារូបត្ថម្ភគ្រប់ទម្រង់ ដើម្បីឈានទៅសម្រេចចក្ខុវិស័យ ស្តីពីប្រព័ន្ធស្បៀងឆ្នាំ២០៣០។,positive
ព្រះអង្គមិនដែលទាមទារអ្វីពីខ្ញុំឡើយ តែព្រះអង្គបានស្រឡាញ់ខ្ញុំជាមុន ហើយក្តីស្រឡាញ់របស់ទ្រង់គឺឥតលក្ខខណ្ឌ,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$
```

How about tail?:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ tail -n 5 ./test.key-word.combine.csv 
ឆ្លងកាត់,neutral
ប្រឡាក់,neutral
ត្រួតពិនិត្យ,neutral
ជិះ,neutral
សង្កេត,neutral
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ tail -n 5 ./test.sentence.combine.csv 
លោកបានបន្ថែមថា រថយន្តបានឆ្លងកាត់ប្រទេសប៊ុលហ្គារី ហ្សកហ្ស៊ី អាមេនី អូសេទីខាងជើង និងតំបន់ Krasnodar របស់រុស្ស៊ី មុនពេលមកដល់លើស្ពាន។​,neutral
ប្រឡាក់អំបិលឲ្យច្រើន ទៅនិងផ្លែម្រះដែលហាន់ជាចំណិតៗ។,neutral
គណៈកម្មាធិការ​នេះ​ មាន​រួម​ប​ញ្ជូ​ល​មន្តរី​មក​ពី​ក្រសួង​ផ្សេងៗ​ ដែល​នឹង​ត្រួតពិនិត្យ​ព័ត៌មាន​ទាក់ទង​នឹង​សុខភាព​ និង​សុវត្ថិភាព​ការងារ​ និង​ផ្តល់​យោបល់​ជូន​រាជរដ្ឋាភិបាល​។,neutral
គ្រានោះមានទ្រមាក់ដំរីម្នាក់ជិះដំរីមកជិតនោះ,neutral
ក្រសួងធនធានទឹក បានលើកឡើងថា៖ «បន្ទាប់ពីបានធ្វើការសង្កេតតាមដានលើស្ថានភាពអាកាសធាតុរួចមក ឃើញថាមានភ្លៀងធ្លាក់ពីតំបន់ជួរភ្នំក្រវាញ ស្ទឹងអារ៉ៃ ស្ទឹងព្រៃខ្លុង និងស្ទឹងធំ មានកម្រិតខ្ពស់ មកលើដងស្ទឹងពោធិ៍សាត់​​​។,neutral
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv$ 
```

## Prepare Final Training/Test Data

Copy path information: 

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv/train.key-word.combine.csv .

(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv/train.sentence.combine.csv .
```

for test data copy path:  
```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv/test.key-word.combine.csv .
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv/test.sentence.combine.csv .

```

## Three Columns Combination:  

Extract each column for training:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cut -f1 -d',' ./train.sentence.combine.csv > ./train.sentence
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cut -f2 -d',' ./train.sentence.combine.csv > ./train.label
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cut -f1 -d',' ./train.key-word.combine.csv > ./train.keyword
```

combination for training data:  
```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ paste -d',' ./train.sentence ./train.keyword ./train.label > train.3col.csv
```

Extract each column for testing:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cut -f1 -d',' ./test.sentence.combine.csv > ./test.sentence
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cut -f2 -d',' ./test.sentence.combine.csv > ./test.label
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cut -f1 -d',' ./test.key-word.combine.csv > ./test.keyword
```

Combination for testing data:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ paste -d',' ./test.sentence ./test.keyword ./test.label > test.3col.csv
```

## Check the Combined Data

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ wc ./train.3col.csv 
   9014   55723 5053854 ./train.3col.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ wc ./test.3col.csv 
  1000   6079 548602 ./test.3col.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ head ./train.3col.csv 
ការ​ឃុំខ្លួន​កញ្ញា សេង ធារី កាន់តែ​យូរ​ដោយ​រដ្ឋាភិបាល​លោក ហ៊ុន សែន នោះ​នឹង​ធ្វើ​ឱ្យ​មនុស្សម្នា​កាន់​តែ​ច្រើន​ដឹងឮ​កាន់តែ​ខ្លាំង​អំពី​របប​ផ្តាច់ការ​នេះ និង​ការណ៍​ដែល​របប​នេះ​ពុំ​មាន​ឆន្ទៈ​អនុញ្ញាត​ឱ្យ​មាន​សំឡេង​នយោបាយ​ប្រឆាំង ព្រមទាំង​វិធី​ដែល​លោក ហ៊ុន សែន រក្សា​អំណាច​ដោយ​ប្រើ​កណ្តាប់​ដៃ​ដែក​របស់​គាត់​។​,ដឹងឮ​កាន់តែ​ខ្លាំង,positive
សូមបញ្ជាក់ថា ក្រុមការងារក្រសួងមហាផ្ទៃបានសហការជាមួយអាជ្ញាធរខេត្តព្រះ សីហនុ បានចុះបង្ករាបទីតាំងល្បែងខុសច្បាប់ចំនួន៥ទីតាំង នៅក្នុងក្រុងព្រះសីហនុ និងបាន រកឃើញជនបរទេសចម្រុះជាតិសាសន៍៕,សហការ,positive
ក្នុងលិខិតបានបញ្ជាក់ថា ក្រុមការងារបង្ករាបមានតួនាទីភារកិច្ចក្នុងការរៀបចំផែនការ វិធានការ គោលការណ៍ណែនាំ ដើម្បីឱ្យអាជ្ញាធរមានសមត្ថកិច្ចគ្រប់លំដាប់ថ្នាក់ អនុវត្តបង្ករាបនូវរាល់ការលេងល្បែងស៊ីសងខុសច្បាប់គ្រប់ប្រភេទ និងត្រូវសហការជាមួយអាជ្ញាធរមានសមត្ថកិច្ចទាំងនៅថ្នាក់ជាតិ រដ្ឋបាលថ្នាក់ក្រោមជាតិ ដើម្បីធ្វើការស្រាវជ្រាវ និងចាត់វិធានការបង្ករាបនូវទីតាំងលេងល្បែងស៊ីសងខុសច្បាប់។,សហការជាមួយអាជ្ញាធរមានសមត្ថកិច្ច,positive
យុវនារីណាដែលកាន់សៀវភៅពេលបច្ចុប្បន្ន គឺនឹងក្លាយទៅជាម្តាយដ៏ល្អនាពេលអនាគត។,ម្តាយដ៏ល្អ,positive
-​ ខ្ញុំ​នៅតែ​នឹក​ នៅ​តែ​ស្រលាញ់​គេ​ ប៉ុន្តែ​ពេល​វេលា​បណ្តាល​ឲ្យ​ខ្ញុំ​បាន​ស្គាល់​មនុស្ស​ល្អ​ម្នាក់​ទៀត​ ដែល​ផ្តល់​រសជាតិ​ជីវិត​មួយ​បែប​ផ្សេង​..,ពេល​វេលា​បណ្តាល​ឲ្យ​ខ្ញុំ​បាន​ស្គាល់​មនុស្ស​ល្អ​,positive
កសិករ​ភាគ​ច្រើន​ក្រៅ​ពី​របរ​ដាំដុះ ពួក​គាត់​តែងតែ​ធ្វើ​ការ​ចិញ្ចឹម​សត្វ គោ ក្របី ជ្រូក មាន់ ទា ពពែ និង​សត្វ​ចៀម​ជា​ដើម ដើម្បី​ជួយ​ដោះស្រាយ​ជីវភាព​គ្រួសារ។​,ជួយ​ដោះស្រាយ​ជីវភាព​គ្រួសារ,positive
បច្ចុប្បន្ន ជនសង្ស័យ​ទាំង​០៣ នាក់ ខាង​លើ ត្រូវ​បាន​កម្លាំង​នគរ​បាល​ការិយាល័យ​ជំនាញ​បញ្ជូន​ទៅ​កាន់​សាលាដំបូង​ខេត្តសៀមរាប ដើម្បី​ចាត់ការ​បន្ត​តាម​នីតិវិធី​ច្បាប់ ។,​ចាត់ការ​បន្ត​តាម​នីតិវិធី​ច្បាប់,positive
ទំនាយទាយថា លោកអ្នកមានរឿងរ៉ាវជាច្រើនដែលត្រូវដោះស្រាយ ប៉ុន្តែបើទោះបីជាដោះមិនបានល្អក្តី ក៏លោកអ្នកនៅតែរក្សាស្ថិរភាពបានជាធម្មតា មិនបង្កបញ្ហាធ្ងន់ធ្ងរអ្វីឡើយ​​​។,រក្សាស្ថិរភាពបានជាធម្មតា/មិនបង្កបញ្ហាធ្ងន់ធ្ងរអ្វីឡើយ​​​,positive
អគ្គលេខាធិការ​ក្លឹប​អង្គ​រថា​យ​ហ្គឺ​រ ដែល​បាន​ដឹកនាំ​យុវជន​ទាំង២​រូប ទៅ​ហ្វឹកហាត់​នៅ​ជប៉ុន លោក អ៊ុំ ករុណា បាននិយាយថា គឺជា​ឱកាស​មាស​សម្រាប់​ពួកគេ ក្នុងការ​សិក្សា​រៀន​សូត្រ និង​ដកស្រង់​បទពិសោធ​ថ្មីៗ​លើ​ទឹកដី​ជប៉ុន ដែលជា​ប្រទេសមួយ​ មានការ​អភិវឌ្ឍ​ខ្លាំង​ផ្នែក​បាល់​ទាត់​​​។,ឱកាស​មាស/ការ​អភិវឌ្ឍ​ខ្លាំង​,positive
ប្រជាពលរដ្ឋ​ខ្មែរ​តែង​មាន​ជំនឿ​ថា ក្នុង​កំឡុង​ពេល​ដែល​យមបាល​ដោះ​លែង​ប្រេត​នោះ ប្រសិនបើ​ប្រេត​ដើរ​រក​គ្រប់​៧​វត្ត​ហើយ​ពុំ​បានឃើញ​មាន​សាច់ញាតិ​របស់​ខ្លួន​ទៅ​វត្ត​ឧទ្ទិស​បុណ្យ​កុសល​ឱ្យ​ទេ​នោះ គឺ​ប្រេត​នឹង​ដាក់​ទំនាយ​ឱ្យ​សាច់ញាតិ​នោះ​ជួប​តែ​រឿង​អាក្រក់ និង​រស់នៅ​ដោយ​គ្មាន​សេចក្តីសុខ​ឡើយ​។,ដាក់​ទំនាយ​/ជួប​តែ​រឿង​អាក្រក់/​រស់នៅ​ដោយ​គ្មាន​សេចក្តីសុខ​,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ head test.3col.csv 
ប៉ុន្តែ​នៅ​ពេល​នេះ​មានការ​សង្កេត​ឃើញ​ថា យុវជន និង​មនុស្ស​វ័យ​កណ្តាល​ដ​ច្រើន បាន​នាំ​គ្នា​សិក្សា​ស្វែង​យល់​ពី​ធម៌​ព្រះពុទ្ធ​ដើម្បី​យក​មក​អនុវត្ត​ផ្ទាល់​នៅ​ក្នុង​ជីវិត​រស់​ប្រចាំ​ថ្ងៃ​។,សិក្សា​ស្វែង​យល់/អនុវត្ត​ផ្ទាល់​,positive
ចំពោះរឿងគ្រួសារ និងស្នេហា គឺល្អប្រសើរ គាប់ចិត្ត គាប់ភ្នែកអ្នកផង៕,ល្អប្រសើរ/គាប់ចិត្ត,positive
បើ​យោង​តាម​ការ​ចុះ​ផ្សាយ​របស់​អង្គការ​កសិករ​ពិភពលោក​ (WFO)​ អំឡុង​ពេល​នៃ​ជំងឺ​រាតត្បាត​កូ​វី​ដ​-១៩​ កសិករ​ក្រីក្រ​បាន​ជួបនឹង​បញ្ហា​ប្រឈម​ក្នុង​ការ​បែងចែក​ប្រាក់​ចំណូល​ដើម្បី​ទុក​ទិញ​ផលិតផល​សុខាភិបាល​ គួប​ផ្សំ​ជាមួយនឹង​ការ​ធ្លាក់​ចុះ​នូវ​វត្តមាន​របស់​ឈ្មួញកណ្តាល​ និង​កង្វះខាត​មធ្យោបាយ​ក្នុង​ការ​ដឹក​ជញ្ជូន​កសិផល​ទៅ​កាន់​ទីផ្សារ​។,​ កសិករ​ក្រីក្រ​បាន​ជួបនឹង​បញ្ហា​ប្រឈម/កង្វះខាត​មធ្យោបាយ,positive
(រាជធានីភ្នំពេញ)៖ ភាគីពាក់ព័ន្ធ ដែលកំពុងធ្វើការយ៉ាងសកម្មលើការលើកកម្ពស់បញ្ហាអាហារូបត្ថម្ភនៅកម្ពុជា បានប្តេជ្ញារួមគ្នា ប្រយុទ្ធនឹងបញ្ហាកង្វះអាហារូបត្ថម្ភគ្រប់ទម្រង់ ដើម្បីឈានទៅសម្រេចចក្ខុវិស័យ ស្តីពីប្រព័ន្ធស្បៀងឆ្នាំ២០៣០។,ប្រយុទ្ធនឹងបញ្ហាកង្វះអាហារូបត្ថម្ភ,positive
ព្រះអង្គមិនដែលទាមទារអ្វីពីខ្ញុំឡើយ តែព្រះអង្គបានស្រឡាញ់ខ្ញុំជាមុន ហើយក្តីស្រឡាញ់របស់ទ្រង់គឺឥតលក្ខខណ្ឌ,ស្រឡាញ់,positive
ប៉ុន្តែ នៅក្នុងទំនាក់ទំនងកម្រិតអ្វីក៏ដោយ បើគេមានភាពស្មោះត្រង់ក្នុងការកសាង «មិត្តភាព» នោះគេនឹងមានការថ្លឹងថ្លែង នឹងមានការក្រែងចំពោះយើង។,ភាពស្មោះត្រង់,positive
ស្របពេលជាមួយគ្នានេះ លោក សេលេស្ត វ៉ាឡាដឺ (Celeste Wallander) មន្តរីជាន់ខ្ពស់មន្ទីរប៉ង់តាហ្គោន បានលើកឡើងថា អ៊ុយក្រែនហាក់ដូចជាកំពុងស្ថិតនៅលើផ្លូវដើម្បីសម្រេចបាននូវគោលដៅសមរភូមិជាច្រើនរបស់ខ្លួន និងបានរំដោះទីតាំងការពារប្រសើរជាងមុន ដើម្បីបញ្ចៀសការប្រយុទ្ធដ៏ក្តៅគគុកក្នុងរដូវរងាខាងមុខនេះ​​​។,បញ្ចៀសការប្រយុទ្ធដ៏ក្តៅគគុក,positive
ប្រព័ន្ធនៃការរៀបចំរបស់អ្នកហុចផលល្អណាស់,ហុចផលល្អណាស់,positive
ដើមឈើប្រណិត និងកម្រទាំងនោះ គួរតែទទួលបានការថែទាំ និងរក្សាទុកនៅកន្លែងដើមរបស់វា។,ទទួលបានការថែទាំ,positive
ឯកឧត្តមបន្តថា កំពង់ផែដែលមានតម្លៃជិត២០លានដុល្លារនេះ នឹងក្លាយចលករដ៏សំខាន់មួយជួយស្រូបទាញអ្នកដំណើរតាមផ្លូវសមុទ្រ ហើយនឹងក្លាយជាច្រកទ្វារអន្តរជាតិដ៏សំខាន់ថ្មីមួយទៀតរបស់កម្ពុជា សម្រាប់ទទួលភ្ញៀវទេសចរជាតិ និងអន្តរជាតិ ដែលមានបំណងធ្វើដំណើររកម្សាន្តតាមផ្លូវទឹករវាងកម្ពុជា ជាមួយបណ្តាប្រទេសក្នុងតំបន់ និងអន្តរជាតិ។​,ចលករដ៏សំខាន់,positive
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ 
```

Check tail part:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ tail -n 3 ./train.3col.csv 
ទាំង​ភោជនីយដ្ឋាន និង​ណូរី​ ត្រូវបាន​សាងសង់​រួចហើយ​តាំងពី​ឆ្នាំ​ ២០២១ ដោយ​ផ្តើម​ទទួលភ្ញៀវ​ជា​ក្រុម​ឯកជន​សម្រាប់តែ​ការ​កក់​ទុក​មុន​។​​​,សាងសង់,neutral
គ្រឿងអេឡិចត្រូនិករបស់យើង បញ្ចេញពន្លឺខៀវ។,បញ្ចេញ,neutral
ចោរនោះធ្វើពុំកើតក៏ក្រាបទូលថា“ខ្ញុំព្រះបាទអម្ចាស់បានពីប្រពន្ធ”,ក្រាបទូល,neutral
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ tail -n 3 ./test.3col.csv 
គណៈកម្មាធិការ​នេះ​ មាន​រួម​ប​ញ្ជូ​ល​មន្តរី​មក​ពី​ក្រសួង​ផ្សេងៗ​ ដែល​នឹង​ត្រួតពិនិត្យ​ព័ត៌មាន​ទាក់ទង​នឹង​សុខភាព​ និង​សុវត្ថិភាព​ការងារ​ និង​ផ្តល់​យោបល់​ជូន​រាជរដ្ឋាភិបាល​។,ត្រួតពិនិត្យ,neutral
គ្រានោះមានទ្រមាក់ដំរីម្នាក់ជិះដំរីមកជិតនោះ,ជិះ,neutral
ក្រសួងធនធានទឹក បានលើកឡើងថា៖ «បន្ទាប់ពីបានធ្វើការសង្កេតតាមដានលើស្ថានភាពអាកាសធាតុរួចមក ឃើញថាមានភ្លៀងធ្លាក់ពីតំបន់ជួរភ្នំក្រវាញ ស្ទឹងអារ៉ៃ ស្ទឹងព្រៃខ្លុង និងស្ទឹងធំ មានកម្រិតខ្ពស់ មកលើដងស្ទឹងពោធិ៍សាត់​​​។,សង្កេត,neutral
```

Shuffling:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ shuf ./train.3col.csv > train.3col.shuf.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ shuf ./test.3col.csv > test.3col.shuf.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ 
```

Final preparation:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp ./train.3col.shuf.csv ./final-data/
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp ./test.3col.shuf.csv ./final-data/

```

Preparing for two experimental setting:  
1) 2 columns only (sentence, label)  
2) 3 columns (sentence, key-word, label)  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cut -f1 -d',' ./train.3col.shuf.csv > train.col1
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cut -f2 -d',' ./train.3col.shuf.csv > train.col2
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cut -f3 -d',' ./train.3col.shuf.csv > train.col3
```

cutting for test data:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cut -f1 -d',' ./test.3col.shuf.csv > test.col1
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cut -f2 -d',' ./test.3col.shuf.csv > test.col2
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cut -f3 -d',' ./test.3col.shuf.csv > test.col3
```

saving under two new folders:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ paste -d',' ./train.col1 ./train.col3 > ./baseline-data/train.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ paste -d',' ./test.col1 ./test.col3 > ./baseline-data/test.csv
```

for experiment with both sentene, keyword:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cp ./train.3col.shuf.csv ./exp-data/train.csv
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cp ./test.3col.shuf.csv ./exp-data/test.csv
```

filesize information:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data$ wc *
   1000    6051  475719 test.csv
   9014   55410 4389874 train.csv
  10014   61461 4865593 total
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data$ cd ..
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data$ cd exp-data/
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$ wc *
   1000    6079  548602 test.csv
   9014   55723 5053854 train.csv
  10014   61802 5602456 total
```

Reconfirm the file content:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data$ head -n 3 {train,test}.csv
==> train.csv <==
សេចក្តី​ត្អូញត្អែរ សេចក្តី​ឈឺចាប់ សេចក្តី​សោក​ស​ង្រែ​ង​សង្រៃ និង​សេចក្តី​អស់សង្ឃឹម​ជា​ទុក្ខ​។,negative
ងូតទឹកធ្លាក់ត្រជាក់ចិត្ត ស្រូបខ្យល់បរិសុទ្ធ ថតរូបស្អាតៗ នៅរមណីយដ្ឋានទឹកធ្លាក់អូរច្រឡង់,positive
លោក ច្រឹ​ក សុខ​នី​ម ប្រធាន​សមាគម​អ្នកវាយតម្លៃ និង​ភ្នា​ក់​ងារ​អចលនវត្ថុ​កម្ពុជាបាន​ប្រាប់ ​ភ្នំពេញ ​ប៉ុស្តិ៍​ថា ក្រៅពី​ចិន និង​ជប៉ុន ដែល​បាន​ចូលរួម​វិ​និ​យោគ​ច្រើន​ក្នុង​វិស័យ​សំណង់​នៅ​កម្ពុជា វិនិយោគិន​នៅ​តំបន់​អឺរ៉ុប ក៏មាន​ការវិនិយោគ​ច្រើន​គួរឱ្យកត់សម្គាល់​ដែរ​។,positive

==> test.csv <==
ទិន្នន័យគយបានបង្ហាញថា នៅចន្លោះខែមករា និងខែសីហាថា ប្រទេសចិនបាននាំចេញប្រេងចម្រាញ់ប្រហែល ១៦,៤ លានតោន ក្នុងនោះរួមមានប្រេងសាំង ៧
នោះគឺ វីរៈបុរសខ្មែរមួយរូបដែលជាស្ថាបនិកសន្តិភាពឈ្មោះ តេជោ ហ៊ុន សែន បានទទួលពានរង្វាន់ «សន្តិភាព ស៊ុនហាក់» ឆ្នាំ២០២២ នៅទីក្រុងសេអ៊ូលនៃ សាធារណៈរដ្ឋកូរ៉េ។,positive
UN ជំរុញឱ្យស្រីលង្កាចាត់វិធានការលើ បញ្ហាសិទ្ធិមនុស្ស ខណៈប្រទេសនេះកំពុងប្រឈមនឹងវិបត្តិសេដ្ឋកិច្ច,negative
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data$ 
```

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$ head -n 3 {train,test}.csv
==> train.csv <==
សេចក្តី​ត្អូញត្អែរ សេចក្តី​ឈឺចាប់ សេចក្តី​សោក​ស​ង្រែ​ង​សង្រៃ និង​សេចក្តី​អស់សង្ឃឹម​ជា​ទុក្ខ​។,​សេចក្តី​ត្អូញត្អែរ/សេចក្តី​ឈឺចាប់/សេចក្តី​សោក​ស​ង្រែ​ង​សង្រៃ/​សេចក្តី​អស់សង្ឃឹម​/ទុក្ខ,negative
ងូតទឹកធ្លាក់ត្រជាក់ចិត្ត ស្រូបខ្យល់បរិសុទ្ធ ថតរូបស្អាតៗ នៅរមណីយដ្ឋានទឹកធ្លាក់អូរច្រឡង់,ងូតទឹកធ្លាក់ត្រជាក់ចិត្ត/ស្រូបខ្យល់បរិសុទ្ធ/ថតរូបស្អាតៗ,positive
លោក ច្រឹ​ក សុខ​នី​ម ប្រធាន​សមាគម​អ្នកវាយតម្លៃ និង​ភ្នា​ក់​ងារ​អចលនវត្ថុ​កម្ពុជាបាន​ប្រាប់ ​ភ្នំពេញ ​ប៉ុស្តិ៍​ថា ក្រៅពី​ចិន និង​ជប៉ុន ដែល​បាន​ចូលរួម​វិ​និ​យោគ​ច្រើន​ក្នុង​វិស័យ​សំណង់​នៅ​កម្ពុជា វិនិយោគិន​នៅ​តំបន់​អឺរ៉ុប ក៏មាន​ការវិនិយោគ​ច្រើន​គួរឱ្យកត់សម្គាល់​ដែរ​។,ការវិនិយោគ​ច្រើន​គួរឱ្យកត់សម្គាល់,positive

==> test.csv <==
ទិន្នន័យគយបានបង្ហាញថា នៅចន្លោះខែមករា និងខែសីហាថា ប្រទេសចិនបាននាំចេញប្រេងចម្រាញ់ប្រហែល ១៦,នាំចេញប្រេងចម្រាញ់,៤ លានតោន ក្នុងនោះរួមមានប្រេងសាំង ៧
នោះគឺ វីរៈបុរសខ្មែរមួយរូបដែលជាស្ថាបនិកសន្តិភាពឈ្មោះ តេជោ ហ៊ុន សែន បានទទួលពានរង្វាន់ «សន្តិភាព ស៊ុនហាក់» ឆ្នាំ២០២២ នៅទីក្រុងសេអ៊ូលនៃ សាធារណៈរដ្ឋកូរ៉េ។,ទទួលពានរង្វាន់,positive
UN ជំរុញឱ្យស្រីលង្កាចាត់វិធានការលើ បញ្ហាសិទ្ធិមនុស្ស ខណៈប្រទេសនេះកំពុងប្រឈមនឹងវិបត្តិសេដ្ឋកិច្ច,ប្រទេសនេះប្រឈមនឹងវិបត្តិសេដ្ឋកិច្ច,negative
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$
```

## SentencePiece Segmentation

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ ls
break.py  kh-segment.model.model  kh-segment.model.vocab  train-sentencepiece.py
```

SentencePiece segmentation for baseline-data:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ python ./break.py ./kh-segment.model.model ./train.col1 > train.col1.sp
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ python ./break.py ./kh-segment.model.model ./test.col1 > test.col1.sp

```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ paste -d',' ./train.col1.sp ./train.col2 > ./train.sp
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ paste -d',' ./test.col1.sp ./test.col2 > ./test.sp

```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ cp train.sp ../train.csv
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data/sentencepiece$ cp test.sp ../test.csv
```

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data$ head -n3 ./train.csv 
▁សេចក្តី ▁ ត ្ អ ូ ញ ត ្ អ ែ រ ▁សេចក្តី ▁ឈឺ ច ាប់ ▁សេចក្តី ▁ស ោក ▁ស ▁ ង ្រ ែ ▁ ង ▁ស ង ្រ ៃ ▁និង ▁សេចក្តី ▁អស់ សង្ឃ ឹម ▁ជា ▁ ទុក្ខ ▁។,negative
▁ ង ូត ទឹក ធ ្ល ាក់ ត្រ ជ ាក់ ចិត្ត ▁ស្រ ូ ប ខ ្យ ល់ ប រ ិ ស ុទ្ធ ▁ ថ ត រ ូ ប ស្ អា ត ៗ ▁នៅ រ ម ណ ី យ ដ្ឋាន ទឹក ធ ្ល ាក់ អ ូរ ច ្រ ឡ ង់,positive
▁លោក ▁ច្រ ឹ ▁ក ▁សុខ ▁ ន ី ▁ម ▁ប្រ ធាន ▁ស មា គ ម ▁អ្នក វ ាយ ត ម្ ល ៃ ▁និង ▁ភ ្ន ា ▁ ក់ ▁ ង ារ ▁អ ច ល ន វត្ថុ ▁កម្ព ុជា បាន ▁ប្រ ាប់ ▁ភ្នំពេ ញ ▁ប៉ ុ ស្ត ិ ៍ ▁ថា ▁ក្រៅ ពី ▁ច ិន ▁និង ▁ជប៉ុន ▁ដែល ▁បាន ▁ ចូលរួម ▁វិ ▁និ ▁ យ ោ គ ▁ច្រើន ▁ក្នុង ▁វិ ស ័យ ▁សំណ ង់ ▁នៅ ▁កម្ព ុជា ▁វិ ន ិ យ ោ គ ិន ▁នៅ ▁តំបន់ ▁អ ឺ រ ៉ ុ ប ▁ក៏ មាន ▁ការ វ ិន ិ យ ោ គ ▁ច្រើន ▁គួរ ឱ្យ ក ត់ ស ម្ គ ាល់ ▁ដែ រ ▁។,positive
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/baseline-data$ head -n3 ./test.csv 
▁ទិន្ន ន ័យ គ យ បាន ប ង ្ ហា ញ ថា ▁នៅ ច ន ្ល ោះ ខ ែម ក រា ▁និង ខ ែ ស ី ហា ថា ▁ប្រទេស ច ិន បាន ន ាំ ចេញ ប្រ េង ច ម្ រ ាញ់ ប្រ ហ ែ ល ▁១ ៦,៤ លានតោន ក្នុងនោះរួមមានប្រេងសាំង ៧
▁នោះ គ ឺ ▁ វី រ ៈ បុរស ខ ្ មែរ មួយ រ ូ ប ដែ ល ជា ស្ ថា ប ន ិក ស ន្ត ិ ភាព ឈ ្ម ោះ ▁ ត េ ជ ោ ▁ ហ៊ុន ▁ស ែន ▁បាន ទ ទ ួល ព ាន រ ង ្វ ាន់ ▁ « ស ន្ត ិ ភាព ▁ស៊ុ ន ហ ាក់ » ▁ឆ្នាំ ២ ០ ២ ២ ▁នៅ ទី ក្រុង ស េ អ ៊ ូល នៃ ▁សា ធ ារ ណ ៈ រ ដ្ឋ ក ូរ ៉ េ ។,positive
▁ UN ▁ជ ំ រ ុ ញ ឱ្យ ស្រី ល ង្ក ា ច ាត់ វិ ធាន ការ លើ ▁បញ្ហា សិទ្ធិ ម ន ុ ស្ស ▁ខណៈ ប្រ ទេស នេះ ក ំ ព ុង ប្រ ឈ ម នឹង វិ ប ត្តិ ស េ ដ្ឋ កិច្ច,negative

```

SentencePiece segmentation for exp-data:  

Extract columns ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece/before-seg$ cut -f1 -d',' ./train.csv > ../train.col1
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece/before-seg$ cut -f2 -d',' ./train.csv > ../train.col2
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece/before-seg$ cut -f3 -d',' ./train.csv > ../train.col3
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece/before-seg$ cut -f1 -d',' ./test.csv > ../test.col1
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece/before-seg$ cut -f2 -d',' ./test.csv > ../test.col2
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece/before-seg$ cut -f3 -d',' ./test.csv > ../test.col3
```

SentencePiece Segmentation:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece$ python ./break.py ./kh-segment.model.model ./train.col1 > train.col1.sp
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece$ python ./break.py ./kh-segment.model.model ./train.col2 > train.col2.sp
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece$ python ./break.py ./kh-segment.model.model ./test.col1 > test.col1.sp
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece$ python ./break.py ./kh-segment.model.model ./test.col2 > test.col2.sp
```

Combination of SentencePice data and label:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece$ paste -d',' ./train.col1.sp ./train.col2.sp ./train.col3 > ../train.csv
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data/sentencepiece$ paste -d',' ./test.col1.sp ./test.col2.sp ./test.col3 > ../test.csv

```

Check the final data:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$ wc *.csv
   1000   85607  645764 test.csv
   9014  788794 5945850 train.csv
  10014  874401 6591614 total
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$ head -n 3 ./train.csv 
▁សេចក្តី ▁ ត ្ អ ូ ញ ត ្ អ ែ រ ▁សេចក្តី ▁ឈឺ ច ាប់ ▁សេចក្តី ▁ស ោក ▁ស ▁ ង ្រ ែ ▁ ង ▁ស ង ្រ ៃ ▁និង ▁សេចក្តី ▁អស់ សង្ឃ ឹម ▁ជា ▁ ទុក្ខ ▁។,▁សេចក្តី ▁ ត ្ អ ូ ញ ត ្ អ ែ រ / ស េ ច ក ្ត ី ▁ឈឺ ច ាប់ / ស េ ច ក ្ត ី ▁ស ោក ▁ស ▁ ង ្រ ែ ▁ ង ▁ស ង ្រ ៃ / ▁សេចក្តី ▁អស់ សង្ឃ ឹម ▁ / ទុក្ខ,negative
▁ ង ូត ទឹក ធ ្ល ាក់ ត្រ ជ ាក់ ចិត្ត ▁ស្រ ូ ប ខ ្យ ល់ ប រ ិ ស ុទ្ធ ▁ ថ ត រ ូ ប ស្ អា ត ៗ ▁នៅ រ ម ណ ី យ ដ្ឋាន ទឹក ធ ្ល ាក់ អ ូរ ច ្រ ឡ ង់,▁ ង ូត ទឹក ធ ្ល ាក់ ត្រ ជ ាក់ ចិត្ត / ស្រ ូ ប ខ ្យ ល់ ប រ ិ ស ុទ្ធ / ថ ត រ ូ ប ស្ អា ត ៗ,positive
▁លោក ▁ច្រ ឹ ▁ក ▁សុខ ▁ ន ី ▁ម ▁ប្រ ធាន ▁ស មា គ ម ▁អ្នក វ ាយ ត ម្ ល ៃ ▁និង ▁ភ ្ន ា ▁ ក់ ▁ ង ារ ▁អ ច ល ន វត្ថុ ▁កម្ព ុជា បាន ▁ប្រ ាប់ ▁ភ្នំពេ ញ ▁ប៉ ុ ស្ត ិ ៍ ▁ថា ▁ក្រៅ ពី ▁ច ិន ▁និង ▁ជប៉ុន ▁ដែល ▁បាន ▁ ចូលរួម ▁វិ ▁និ ▁ យ ោ គ ▁ច្រើន ▁ក្នុង ▁វិ ស ័យ ▁សំណ ង់ ▁នៅ ▁កម្ព ុជា ▁វិ ន ិ យ ោ គ ិន ▁នៅ ▁តំបន់ ▁អ ឺ រ ៉ ុ ប ▁ក៏ មាន ▁ការ វ ិន ិ យ ោ គ ▁ច្រើន ▁គួរ ឱ្យ ក ត់ ស ម្ គ ាល់ ▁ដែ រ ▁។,▁ការ វ ិន ិ យ ោ គ ▁ច្រើន ▁គួរ ឱ្យ ក ត់ ស ម្ គ ាល់,positive
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$ head -n 3 ./test.csv
▁ទិន្ន ន ័យ គ យ បាន ប ង ្ ហា ញ ថា ▁នៅ ច ន ្ល ោះ ខ ែម ក រា ▁និង ខ ែ ស ី ហា ថា ▁ប្រទេស ច ិន បាន ន ាំ ចេញ ប្រ េង ច ម្ រ ាញ់ ប្រ ហ ែ ល ▁១ ៦,▁នាំ ចេញ ប្រ េង ច ម្ រ ាញ់,៤ លានតោន ក្នុងនោះរួមមានប្រេងសាំង ៧
▁នោះ គ ឺ ▁ វី រ ៈ បុរស ខ ្ មែរ មួយ រ ូ ប ដែ ល ជា ស្ ថា ប ន ិក ស ន្ត ិ ភាព ឈ ្ម ោះ ▁ ត េ ជ ោ ▁ ហ៊ុន ▁ស ែន ▁បាន ទ ទ ួល ព ាន រ ង ្វ ាន់ ▁ « ស ន្ត ិ ភាព ▁ស៊ុ ន ហ ាក់ » ▁ឆ្នាំ ២ ០ ២ ២ ▁នៅ ទី ក្រុង ស េ អ ៊ ូល នៃ ▁សា ធ ារ ណ ៈ រ ដ្ឋ ក ូរ ៉ េ ។,▁ទទួល ព ាន រ ង ្វ ាន់,positive
▁ UN ▁ជ ំ រ ុ ញ ឱ្យ ស្រី ល ង្ក ា ច ាត់ វិ ធាន ការ លើ ▁បញ្ហា សិទ្ធិ ម ន ុ ស្ស ▁ខណៈ ប្រ ទេស នេះ ក ំ ព ុង ប្រ ឈ ម នឹង វិ ប ត្តិ ស េ ដ្ឋ កិច្ច,▁ប្រទេស នេះ ប្រ ឈ ម នឹង វិ ប ត្តិ ស េ ដ្ឋ កិច្ច,negative
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/final-data/exp-data$
```

Copied to server ...  

## Training with Two Columns Data
  
When strat training with SentencePiece data, got following error:  

```
<class 'torch.nn.modules.activation.Tanh'>], 'choice_values_used': ["<class 'torch.nn.modules.activation.Tanh'>", "<class 'torch.nn.modules.linear.Identity'>", '<function get_diff_causal.<locals>.<lambda> at 0x7fc575dfb670>', "<class 'torch.nn.modules.activation.ELU'>"]}, 'block_wise_dropout': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sort_features': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
Traceback (most recent call last):
  File "./khpolar-tabpfn-baseline.py", line 59, in <module>
    classifier.fit(X_train, y_train)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 164, in fit
    y = self._validate_targets(y)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py", line 148, in _validate_targets
    check_classification_targets(y)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/utils/multiclass.py", line 189, in check_classification_targets
    y_type = type_of_target(y)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/sklearn/utils/multiclass.py", line 327, in type_of_target
    if (len(np.unique(y)) > 2) or (y.ndim >= 2 and len(y[0]) > 1):
  File "<__array_function__ internals>", line 6, in unique
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/numpy/lib/arraysetops.py", line 272, in unique
    ret = _unique1d(ar, return_index, return_inverse, return_counts)
  File "/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/numpy/lib/arraysetops.py", line 333, in _unique1d
    ar.sort()
TypeError: '<' not supported between instances of 'str' and 'float'

real	0m3.945s
user	0m2.092s
sys	0m2.309s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$
```

Recheck the no. of lines for each column:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/final-data/baseline-data$ cut -f1 -d ',' ./train.csv | wc
   9015  687601 5035452
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/final-data/baseline-data$ cut -f2 -d ',' ./train.csv | wc
   9015    9662  123681
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/final-data/baseline-data$ cut -f1 -d ',' ./test.csv | wc
   1001   74421  544057
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/final-data/baseline-data$ cut -f2 -d ',' ./test.csv | wc
   1001    1085   15311
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/final-data/baseline-data$
```

Although number of lines are equal, I found the problem as follows:  

```
label
៤ លានតោន ក្នុងនោះរួមមានប្រេងសាំង ៧
positive
negative
positive
positive
positive
positive
negative
 លោកអគ្គលេខាធិការអាស៊ាន ពីការកើនឡើងនៃសេចក្តីត្រូវការថាមពល និងអស្ថិរភាពនៃថ្លៃប្រេងឥន្ធនៈ នៅលើទីផ្សារអន្តរជាតិ បាននិងកំពុងបង្កឱ្យមានអតិផរណាខ្ពស់
negative
negative
```

--------

## Preparing 3 types of Training/Test Dataset

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv/train.sentence.combine.csv .

(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/train/csv/train.key-word.combine.csv .

(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv/test.sentence.combine.csv .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ cp /media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final/shuffle/split-data/split-class/test/csv/test.key-word.combine.csv .
```

check filesize:  
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ wc *
     10      22     992 note.txt
   1000    1028   81791 test.key-word.combine.csv
   1000    6086  478200 test.sentence.combine.csv
   9014    9327  744276 train.key-word.combine.csv
   9014   55743 4407928 train.sentence.combine.csv
  20038   72206 5713187 total

(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ rev train.key-word.combine.csv | cut -f1 -d',' | rev > train.label
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ rev test.key-word.combine.csv | cut -f1 -d',' | rev > test.label

(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ rev train.key-word.combine.csv | cut -f2- -d"," | rev > train.keyword
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ rev test.key-word.combine.csv | cut -f2- -d"," | rev > test.keyword

(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ rev train.sentence.combine.csv | cut -f2- -d"," | rev > train.sentence
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ rev test.sentence.combine.csv | cut -f2- -d"," | rev > test.sentence
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$
```

Cleaning process:  

```
313 comma inside train.sentence (replaced with NULL)
35 comma inside test.sentence (replaced with NULL)
```

Combine:   

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ paste train.sentence train.keyword ./train.label > ./shuffle/train.combine
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ paste test.sentence test.keyword ./test.label > ./shuffle/test.combine
```

Shuffle:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ shuf ./train.combine > train.combine.shuf
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ shuf ./test.combine > test.combine.shuf
```

Extracted fields from shuffle data:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ cut -f1 ./train.combine.shuf > train.combine.shuf.f1
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ cut -f2 ./train.combine.shuf > train.combine.shuf.f2
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ cut -f3 ./train.combine.shuf > train.combine.shuf.f3
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ cut -f1 ./test.combine.shuf > test.combine.shuf.f1
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ cut -f2 ./test.combine.shuf > test.combine.shuf.f2
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ cut -f3 ./test.combine.shuf > test.combine.shuf.f3
```

Check filesize:   
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ wc train.combine.shuf.{f1,f2,f3}
   9014   55742 4327319 train.combine.shuf.f1
   9014    9327  663980 train.combine.shuf.f2
   9014    9014   80296 train.combine.shuf.f3
  27042   74083 5071595 total
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ wc test.combine.shuf.{f1,f2,f3}
  1000   6085 469257 test.combine.shuf.f1
  1000   1028  72883 test.combine.shuf.f2
  1000   1000   8908 test.combine.shuf.f3
  3000   8113 551048 total
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ 
```

## Prepare Baseline and Experiment Dataset

Prepare baseline-sentence data:  
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ paste -d',' train.combine.shuf.f1 train.combine.shuf.f3 > ../baseline-sentence/train.csv
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ paste -d',' test.combine.shuf.f1 test.combine.shuf.f3 > ../baseline-sentence/test.csv
```

Prepare baseline-keyword data: 
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ paste -d',' train.combine.shuf.f2 train.combine.shuf.f3 > ../baseline-keyword/train.csv
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ paste -d',' test.combine.shuf.f2 test.combine.shuf.f3 > ../baseline-keyword/test.csv
```

Prepare experiment data:  
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ paste -d',' train.combine.shuf.f1 train.combine.shuf.f2 train.combine.shuf.f3 > ../exp/train.csv
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess/shuffle$ paste -d',' test.combine.shuf.f1 test.combine.shuf.f2 test.combine.shuf.f3 > ../exp/test.csv
```

Check the folder structure: 
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ tree {baseline-keyword,baseline-sentence,exp}
baseline-keyword
├── test.csv
└── train.csv
baseline-sentence
├── test.csv
└── train.csv
exp
├── test.csv
└── train.csv

0 directories, 6 files
```

Check the filesize again:  
```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-final/preprocess$ wc {baseline-keyword,baseline-sentence,exp}/*.csv
    1000     1028    81791 baseline-keyword/test.csv
    9014     9327   744276 baseline-keyword/train.csv
    1000     6085   478165 baseline-sentence/test.csv
    9014    55742  4407615 baseline-sentence/train.csv
    1000     6113   551048 exp/test.csv
    9014    56055  5071595 exp/train.csv
```

----------------

## Training with Baseline-Sentence

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn-baseline.py
...
...
...
ues': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Baseline-Sentence Accuracy: 0.583

real	1m27.940s
user	12m15.163s
sys	2m41.673s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ 
```

## Training with Baseline-Keyword

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn-baseline.py 
...
...
...
ues': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Baseline-Keyword Accuracy: 0.583

real	1m28.024s
user	12m15.379s
sys	2m43.325s
```

## Training with Both Sentence and Keyword

```
ues': [True, False]}, 'in_clique': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Experiment with Both Sent+Keyword Accuracy: 0.583

real	2m47.823s
user	24m20.455s
sys	5m7.098s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn-baseline.py 
```

The results are strange and I am thinking ...  
Currently, Using normal or natural Khmer sentence and I plan to use SentencePiece ...  

## SentencePiece Data Info

I did SentencePiece Segmentation and the updated data info is as follows:  

for Baseline-keyword:  

```
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-keyword$ ls
test.csv  tmp  train.csv  word
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-keyword$ head -n 5 *.csv
==> test.csv <==
keyword,label
▁ប្រ សា ស ន៍,negative
▁ប ន ្ល ំ ▁ការ ▁ពិ ត,negative
▁មាន ស្ ថ ិ រ ភាព,positive
▁កាត់ បន្ថ យ ការ វិ វ ត្ត ន៍ រ ប ស់ ជ ំ ង ឺ,positive
▁លក្ខណៈ ធ ម្មតា,neutral

==> train.csv <==
keyword,label
▁ការ គ ំ រា មក ំ ហ ែង,negative
▁ចាប់ ផ្តើម ប្រ ើ,neutral
▁ហ ែ ល,neutral
▁កាត់ បន្ថ យ អ ត្រា ស្លាប់ រ ប ស់ ក ្ម េង យ៉ា ង ច្រើន,positive
▁ការ ចូលរួម ល ះ ប ង់ ជ ្រោម ជ ្រ ែង ទ ាំង ស ង ខាង / ស ុ ភ ម ង្គ ល,positive
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-keyword$
```
```
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-keyword$ wc *.csv
  1000  12095  95315 test.csv
  9014 109470 867024 train.csv
 10014 121565 962339 total
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-keyword$
```

for baseline-sentence:  
```
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-sentence$ ls
test.csv  tmp  train.csv  word
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-sentence$ head -n3 *.csv
==> test.csv <==
sentence,label
▁ នេះ ប ើ តា ម ប្រ សា ស ន៍ រ ប ស់ ▁ឯក ឧ ត្ត ម ▁ ន េ ត្រ ▁ភ ក ្ត រា ▁រដ្ឋ លេខ ា ធ ិ ការ ▁និង ជា អ ន ុ ប្រ ធាន អ ច ិ ន្ត រ ៃ យ ៍ ក្រ ុ ម ការ ង ារ ប្រឆាំង ការ ស ម្ អា ត ប្រ ាក់ នៃ ក្រ ស ួង ប រ ិ ស្ថាន ▁កាល ថ ្ ង ៃ ទី ៥ ▁ខែ ត ុល ា ▁ឆ្នាំ ២ ០ ២ ២ ▁។,negative
▁ចំណ ែក ▁ម ន្ត រី ▁ សិទ្ធិ ម ន ុ ស្ស ▁និង ▁អ្នក វិ ភ ា គ ▁យល់ ▁ថា ▁អ្វី ▁ដែល ▁លោក ▁ ហ៊ុន ▁ស ែន ▁លើក ▁ឡើង ▁មក ▁នោះ ▁ជា ▁វ ោ ហា រ សា ស្ត រ ▁ ន យោប ាយ ▁ដើម្បី ▁ប ន ្ល ំ ▁ការ ▁ពិ ត ▁ប៉ុណ្ណ ោះ ។,negative
▁ការងា រ មាន ស្ ថ ិ រ ភាព ▁ហើយ អ ្ន ក អា ច ទ ទ ួល បាន ស ម ិទ្ធ ផល ជ ាក់ ល ាក់ ក្នុង អា ជ ី ព រ ប ស់ អ ្ន ក ▁ ធាន ា ជ ី វ ិត រ ប ស់ អ ្ន ក ។,positive

==> train.csv <==
sentence,label
▁រដ្ឋ ម ន្ត រី ប រ ិ ស្ថាន អ ៊ ុយ ក្រ ែន បាន បញ្ជា ក់ កាល ពី ថ ្ ង ៃ ច ន្ទ ទី ▁៣ ▁ខែ ត ុល ា ថា ▁ការ ខ ូ ច ខាត ប រ ិ ស្ថាន ក្នុង ប្រ ទេស អ ៊ ុយ ក្រ ែន ដែ ល ប ណ្តាល មក ពី ការ ឈ ្ល ាន ព ាន រ ប ស់ រ ុ ស្ ស៊ី ត្រ ូវ បាន គេ ប៉ ាន់ ប្រ មា ណ ថា ▁មាន ទ ំ ហ ំ ជា ង ▁៣ ៥ ៣ ព ាន់ ល ាន ដ ុល ្ល ារ ▁ជាមួយ នឹង ត ំ ប ន់ អ ភ ិ រ ក្ស ធ ម្ ម ជាតិ រ ាប់ ល ាន ហ ិក តា ទ ៀ ត ស្ ថ ិត ន ៅ ក ្រោម ការ គ ំ រា មក ំ ហ ែង ▁។,negative
▁ខ្ញុំ ច ង់ ច ាប់ ផ្តើម ប្រ ើ ផ ា ស ពិសេស ស ំ រ ាប់ អ ្ន ក ធ្វើដំណើរ,neutral
▁ក្រោយ ពេល ដែ ល វា បាន ហ ែ ល ប ត់ ច ុះ ប ត់ ឡើង គ ្រ ប់ ៗ ក ន ្ល ែង វា ទៅ ដល់ ស្រ ុក ខ ោ ន ហើយ វា ស ំ ច ត ន ៅ ទី នោះ ២ . ២ ថ ្ ង ៃ ទ ើ ប វា ហ ែ ល ច ុះ មក វិញ ។,neutral
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-sentence$
```

filesize info:  

```
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-sentence$ wc *.csv
   1000   75892  563439 test.csv
   9014  698067 5188704 train.csv
  10014  773959 5752143 total
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/baseline-sentence$
```

for exp:  

```
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/exp$ ls
test.csv  tmp  train.csv  word
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/exp$ head -n3 *.csv
==> test.csv <==
sentence,keyword,label
▁ នេះ ប ើ តា ម ប្រ សា ស ន៍ រ ប ស់ ▁ឯក ឧ ត្ត ម ▁ ន េ ត្រ ▁ភ ក ្ត រា ▁រដ្ឋ លេខ ា ធ ិ ការ ▁និង ជា អ ន ុ ប្រ ធាន អ ច ិ ន្ត រ ៃ យ ៍ ក្រ ុ ម ការ ង ារ ប្រឆាំង ការ ស ម្ អា ត ប្រ ាក់ នៃ ក្រ ស ួង ប រ ិ ស្ថាន ▁កាល ថ ្ ង ៃ ទី ៥ ▁ខែ ត ុល ា ▁ឆ្នាំ ២ ០ ២ ២ ▁។,▁ប្រ សា ស ន៍,negative
▁ចំណ ែក ▁ម ន្ត រី ▁ សិទ្ធិ ម ន ុ ស្ស ▁និង ▁អ្នក វិ ភ ា គ ▁យល់ ▁ថា ▁អ្វី ▁ដែល ▁លោក ▁ ហ៊ុន ▁ស ែន ▁លើក ▁ឡើង ▁មក ▁នោះ ▁ជា ▁វ ោ ហា រ សា ស្ត រ ▁ ន យោប ាយ ▁ដើម្បី ▁ប ន ្ល ំ ▁ការ ▁ពិ ត ▁ប៉ុណ្ណ ោះ ។,▁ប ន ្ល ំ ▁ការ ▁ពិ ត,negative
▁ការងា រ មាន ស្ ថ ិ រ ភាព ▁ហើយ អ ្ន ក អា ច ទ ទ ួល បាន ស ម ិទ្ធ ផល ជ ាក់ ល ាក់ ក្នុង អា ជ ី ព រ ប ស់ អ ្ន ក ▁ ធាន ា ជ ី វ ិត រ ប ស់ អ ្ន ក ។,▁មាន ស្ ថ ិ រ ភាព,positive

==> train.csv <==
sentence,keyword,label
▁រដ្ឋ ម ន្ត រី ប រ ិ ស្ថាន អ ៊ ុយ ក្រ ែន បាន បញ្ជា ក់ កាល ពី ថ ្ ង ៃ ច ន្ទ ទី ▁៣ ▁ខែ ត ុល ា ថា ▁ការ ខ ូ ច ខាត ប រ ិ ស្ថាន ក្នុង ប្រ ទេស អ ៊ ុយ ក្រ ែន ដែ ល ប ណ្តាល មក ពី ការ ឈ ្ល ាន ព ាន រ ប ស់ រ ុ ស្ ស៊ី ត្រ ូវ បាន គេ ប៉ ាន់ ប្រ មា ណ ថា ▁មាន ទ ំ ហ ំ ជា ង ▁៣ ៥ ៣ ព ាន់ ល ាន ដ ុល ្ល ារ ▁ជាមួយ នឹង ត ំ ប ន់ អ ភ ិ រ ក្ស ធ ម្ ម ជាតិ រ ាប់ ល ាន ហ ិក តា ទ ៀ ត ស្ ថ ិត ន ៅ ក ្រោម ការ គ ំ រា មក ំ ហ ែង ▁។,▁ការ គ ំ រា មក ំ ហ ែង,negative
▁ខ្ញុំ ច ង់ ច ាប់ ផ្តើម ប្រ ើ ផ ា ស ពិសេស ស ំ រ ាប់ អ ្ន ក ធ្វើដំណើរ,▁ចាប់ ផ្តើម ប្រ ើ,neutral
▁ក្រោយ ពេល ដែ ល វា បាន ហ ែ ល ប ត់ ច ុះ ប ត់ ឡើង គ ្រ ប់ ៗ ក ន ្ល ែង វា ទៅ ដល់ ស្រ ុក ខ ោ ន ហើយ វា ស ំ ច ត ន ៅ ទី នោះ ២ . ២ ថ ្ ង ៃ ទ ើ ប វា ហ ែ ល ច ុះ មក វិញ ។,▁ហ ែ ល,neutral
```

```
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/exp$ wc *.csv
   1000   86987  649846 test.csv
   9014  798523 5975432 train.csv
  10014  885510 6625278 total
yekyaw.thu@gpu:~/exp/kh-polar/kh-final-sp/exp$
```

## Training Again  

training with sentence only:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn-baseline.py
...
...
...
alues': [True, False]}, 'sampling': {'distribution': 'meta_choice', 'choice_values': ['normal', 'mixed']}, 'pre_sample_causes': {'distribution': 'meta_choice', 'choice_values': [True, False]}, 'outputscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Baseline-Keyword Accuracy: 0.583

real    1m26.543s
user    12m13.920s
sys     2m39.558s
```

training with keyword only:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn-baseline.py
...
...
...
ale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'lengthscale': {'distribution': 'meta_trunc_norm_log_scaled', 'max_mean': 10.0, 'min_mean': 1e-05, 'round': False, 'lower_bound': 0}, 'noise': {'distribution': 'meta_choice', 'choice_values': [1e-05, 0.0001, 0.01]}, 'multiclass_type': {'distribution': 'meta_choice', 'choice_values': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Baseline-Keyword Accuracy: 0.583

real    1m26.073s
user    12m14.297s
sys     2m34.845s 
```

See Not improving ...  

Training with sentence,keyword,label ...  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ time python ./khpolar-tabpfn-baseline.py
...
...
...
es': ['value', 'rank']}}}, 'num_features': 100, 'epoch_count': 0}
Style definition of first 3 examples: None
Using a Transformer with 25.82 M parameters
/home/yekyaw.thu/.conda/envs/tabpfn/lib/python3.7/site-packages/tabpfn/scripts/transformer_prediction_interface.py:147: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().
  y_ = column_or_1d(y, warn=True)
⚠️ WARNING: TabPFN is not made for datasets with a trainingsize > 1024. Prediction might take a while and be less reliable.
Baseline-Keyword Accuracy: 0.583

real    2m46.758s
user    24m21.226s
sys     5m1.476s 
```

## Write a Python Code for Khmer Text to tf-idf Conversion

```python
from sklearn.feature_extraction.text import TfidfVectorizer
import sys
import pandas as pd
import re

# Written by Ye Kyaw Thu, Affiliate Professor, IDRI, CADT, Cambodia
# Calculating syllable tf-idf
# Last updated: 25 Sept 2022
# How to run:
# $ python ./syl2tf-idf.py ./eg-corpus.txt
#
# References
# https://github.com/gearmonkey/tfidf-python/blob/master/tfidf.py
# https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfTransformer.html#:~:text=The%20formula%20that%20is%20used,document%20frequency%20of%20t%3B%20the

def dummy_break(line):
   return line.split()

with open(sys.argv[1]) as f:
    corpus = f.read().splitlines()

# Add a custom list of stopwords for punctuation
# 'ៗ' 
kh_stop_words = ['។', '៕', '៖', '«', '»', '&', '"', '!', '?', '(', ')', '-', '.', '/', ':', ';', '[', ']']

vectorizer = TfidfVectorizer(tokenizer=dummy_break, stop_words=kh_stop_words, use_idf=True, norm='l2') # l2 normalizer is the default normalizer
#vectorizer = TfidfVectorizer(stop_words=my_stop_words, tokenizer=sylbreak_my, use_idf=True, norm='l1') # for seeing with l1 normalizer result
matrix = vectorizer.fit_transform(corpus)
sp_tf_idf = pd.DataFrame(matrix.toarray(), columns=vectorizer.get_feature_names_out())
print(sp_tf_idf)
```

Test run with above Python code:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/tfidf$ python ./sp2tf-idf.py ./test.f1 
       %    2  202  2022  2023    5    a  ...  ▁១៩   ▁២  ▁២០១   ▁៣   ▁៤   ▁៥    ➎
0    0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
1    0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
2    0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
3    0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
4    0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
..   ...  ...  ...   ...   ...  ...  ...  ...  ...  ...   ...  ...  ...  ...  ...
995  0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
996  0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
997  0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
998  0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0
999  0.0  0.0  0.0   0.0   0.0  0.0  0.0  ...  0.0  0.0   0.0  0.0  0.0  0.0  0.0

[1000 rows x 1152 columns]
```

Test run with big data (training data):  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/tfidf$ python ./sp2tf-idf.py ./train.f1 
        #    $  $98    %   &d    *    +  ...   ▁៥    ➊    ➋    ➌    ➍    ➏    👉
0     0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
1     0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
2     0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
3     0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
4     0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
...   ...  ...  ...  ...  ...  ...  ...  ...  ...  ...  ...  ...  ...  ...  ...
9010  0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
9011  0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
9012  0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
9013  0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0
9014  0.0  0.0  0.0  0.0  0.0  0.0  0.0  ...  0.0  0.0  0.0  0.0  0.0  0.0  0.0

[9015 rows x 2453 columns]
```

I updated the stop-word list as follows:  

```python
kh_stop_words = ['។', '៕', '៖', '«', '»', '&', '"', '!', '?', '(', ')', '-', '.', '/', ':', ';', '[', ']', '$', '#','*', '+', '➊', '➋', '➌', '➍', '➏', '👉', '&d']
```

Run with big data file (i.e. training data) again:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/tfidf$ python ./sp2tf-idf.py ./train.f1 
      $98    %    0  000000    1   10  ...  ▁១៩   ▁២  ▁២០១        ▁៣        ▁៤   ▁៥
0     0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
1     0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.228228  0.000000  0.0
2     0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
3     0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
4     0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
...   ...  ...  ...     ...  ...  ...  ...  ...  ...   ...       ...       ...  ...
9010  0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
9011  0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
9012  0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0
9013  0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.218761  0.0
9014  0.0  0.0  0.0     0.0  0.0  0.0  ...  0.0  0.0   0.0  0.000000  0.000000  0.0

[9015 rows x 2442 columns]
```

## Python Code for SentencePiece to Word2Vec

Actually, the following program can use with any segmentation unit. Here, we are building a Word2Vec model with SentencePiece Model and thus, I titled as SentencePiece to WordVec ...  

```python
import sys
import gensim.models

# Written by Ye Kyaw Thu, Affiliate Professor, IDRI, CADT, Cambodia
# Word2Vec model building for segmented text file.
# input file က စာကြောင်း တစ်ကြောင်းစီ ရိုက်ထားပြီးတော့ 
# စာလုံး (e.g. word or syllable) ဖြတ်ထားပြီးသား ဖြစ်ရမယ်
#
# Last updated: 6 Oct 2022
# How to run:
# ./word2vec.py <corpus-file> <model-file> <bin|txt>
# python ./word2vec.py ../mypos-ver.3.0.word.txt w2v.model.bin bin
# python ./word2vec.py ../mypos-ver.3.0.word.txt w2v.model.txt txt

# References:
# Tomas Mikolov, Kai Chen, Greg Corrado, and Jeffrey Dean. 2013a. Efficient estimation of word representations in vector space. arXiv preprint arXiv:1301.3781.
# https://pypi.org/project/gensim/

training_corpus = sys.argv[1]
model_filename = sys.argv[2]
filetype = sys.argv[3]

with open(training_corpus,'r') as f:
    plain_text = f.read()

sentences = plain_text.split("\n")  # Assume one sentence per line
tokenized = []

for sentence in sentences:
    # White-space-based word splitting, replace with a better tokenizer
    tokens = sentence.strip().split(' ')
    tokenized.append(tokens)

# Here, sample for subsampling rate, negative for negative samples, min_count for minimum threshold, workers for parallelize to all cores, hs=0 for no hierarchical softmax
# default values min_count is 5, workers=1
model = gensim.models.Word2Vec(sentences=tokenized, vector_size=100, window=3, sample=0.01, epochs=10, negative=3, min_count=2, workers=1, hs=0)

if (filetype == "bin"):
   model.save(model_filename)
elif (filetype == "txt"):
   model.wv.save_word2vec_format(model_filename, binary= False, write_header= False)
```

Building word2vec model ...  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/fasttext$ python ./word2vec.py ./train.f1 train.f1.w2v bin
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/fasttext$ python ./word2vec.py ./train.f1 train.f1.w2v.txt txt
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/fasttext$ ls train.f1.w2v*
train.f1.w2v  train.f1.w2v.txt
```

Let's check the text format of Word2Vec model:  

```
(sentiment) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/fasttext$ head train.f1.w2v.txt 
រ -0.3452834 1.0565568 1.1130344 0.85697764 1.4965903 1.9389682 -0.049469355 -0.84155345 -0.16357906 1.8787647 -0.23838553 1.1239814 -1.9010674 -1.8762144 -2.43517 -1.4837047 1.1950661 0.7704238 -2.8337576 -0.830489 1.0049344 1.5111798 -1.4751089 1.8826463 1.8625243 1.0827092 0.69890225 3.0591989 -2.501259 0.60925245 -2.2505221 0.24505919 0.51306844 -1.6449277 -0.27436075 -3.0877254 2.722921 -1.4953113 2.717628 0.47590435 -2.101622 0.0029691362 -3.7294495 1.0547869 -1.1686928 -0.98752713 -0.6088379 0.25170118 2.4956574 -1.1565049 -1.9682378 3.7590263 -0.3154171 -2.452455 0.75954837 -1.2359698 -0.21879242 -0.7065108 -0.25629652 2.314593 0.512223 -0.64464 -1.174108 -0.45083493 1.3635247 -0.41838148 0.18022648 -0.6567169 -0.7434361 0.44802892 -0.49911988 1.562051 -0.52891874 -1.6370343 -1.21087 -0.6286243 3.704315 0.6792467 -1.0555844 0.1763148 -1.8504611 -0.7505143 -1.1684155 -0.6343142 -1.7535566 -2.4641008 2.0533683 -1.084172 -0.65342444 0.08926606 1.7207853 1.9456942 2.6059508 -0.15972434 2.5581753 2.071199 -1.370767 0.15206343 -0.05997989 1.6760896
ប -2.5267932 0.895098 -1.1690494 1.1344312 0.8657275 1.5112509 0.81179196 2.0063014 -0.18939967 -1.4400909 -1.6892781 -2.258639 0.048910078 -1.7891884 0.82864183 0.7593218 1.5158372 1.0541115 -1.7548901 -0.27728495 0.3779317 0.22799379 0.02807444 0.17776023 0.72880894 0.74800044 1.1838207 0.66844046 0.42383856 -0.80070144 1.2123147 -2.3617785 0.054625414 1.2946671 -2.4011655 -0.41188136 2.0760517 1.122372 2.65108 1.179943 -1.4002506 1.5388881 -2.1539516 2.3575246 -0.59428304 1.9721317 0.9843023 -1.753785 1.227864 1.3079506 0.41868287 -1.3633112 -2.31441 -1.6965584 1.6198804 -1.694204 -2.2321942 1.2576121 -2.2862203 0.92810893 0.3886364 0.2252481 1.334888 0.900939 -1.0894177 0.47502324 3.1875913 -1.3570083 2.2765014 -0.041204453 1.3283579 -1.3674766 3.487943 2.2649226 -3.0540254 2.1747582 1.6339204 -0.5579168 0.5935114 1.013281 -2.1879535 1.0177617 1.6105642 -2.9213362 -0.3808309 -3.254929 0.69956255 0.56297714 -0.8726801 -1.0355443 2.2573035 0.9016079 2.8002858 -3.4228733 1.5786057 3.094336 1.2327632 -1.2699755 0.3598945 0.0091602355
▁ 0.3751662 -0.53149015 0.33619192 0.071723685 -1.8321728 0.35620087 -1.0245694 -1.655044 0.9924197 -1.2049019 1.2588837 0.6357223 -0.15842257 -0.47426143 0.46891952 0.09109473 -1.3415977 2.397506 0.30185243 2.0226789 -1.1063282 -0.41274786 -0.2520502 -0.35831243 0.5001628 -0.07127925 0.74898714 -0.9123425 0.31770912 0.69033736 -1.2642272 0.0074880947 0.76707315 -1.0959015 0.8474288 -1.9194965 -0.52399004 0.6561188 -0.77175456 1.928875 1.5459442 0.022053467 1.2452712 -0.8199412 -0.7540815 2.1136343 1.3350376 -1.247241 -0.26839784 1.1016899 0.82213104 -1.4534283 -0.87134516 -0.70368254 -0.47245988 0.4296103 1.4047109 -0.8039361 2.7056856 0.4236756 -1.3924541 1.0676166 -1.1607925 0.45881715 0.42505747 0.73391116 2.2099931 -0.12733278 1.5683974 -0.28438354 1.4668969 -0.51875675 -2.0541863 -0.89553446 0.50429726 -1.1637585 -0.69935346 -0.3928311 1.0564218 -0.048689455 1.9938012 -0.6585552 -0.9345896 0.37180832 1.474649 1.8357724 -1.9942869 -1.905857 -0.19879006 -1.7397811 -1.3303987 -0.10871308 -1.3622816 0.6243021 -2.2407527 -1.826616 0.26349708 0.9059224 -2.1921535 -0.09927535
ក 0.8983983 1.5388368 -1.5405514 -1.033761 0.8624194 2.304958 -1.85384 1.5962031 0.34413758 0.49614152 -1.0911916 1.7339948 -1.4894128 -1.2214589 2.6382434 -1.2458556 2.6460319 -1.4201179 -0.34010634 1.3201596 1.7810432 -1.6700528 2.6423824 1.0994548 -1.8891147 -0.92629164 2.4092517 1.7627653 0.78746 0.061476927 -1.043777 -1.7368436 -1.6740506 0.042319465 0.7965063 -0.64821887 2.152011 0.3166852 -0.3362032 3.3837755 -0.12114155 3.1549628 -0.7081114 0.9219022 2.0511794 3.0348155 -0.53811496 1.7353313 -1.4747787 -1.3169143 -2.4137273 -0.16028391 -1.5558035 -0.65856886 -0.8409368 0.19639222 -1.654977 0.08361582 -0.49985412 -1.1503848 0.16760963 0.13376135 3.1038077 -2.106251 0.13272245 -0.67094463 1.2934867 1.8548722 0.2910647 -2.2337568 0.9890432 1.068665 2.4330988 1.2490847 -1.737379 0.7482672 0.7408024 1.6590401 -1.2983456 1.9965422 0.41368774 -0.24713928 -0.33680132 1.0247678 -1.43414 -1.5221335 1.0963229 1.0658563 -0.4064008 -1.020606 -0.2296137 1.1854216 1.299603 -3.138552 1.5369109 1.693652 2.0225458 0.44632226 1.2933325 -2.0523655
ន -3.922742 1.1012222 -2.76371 0.5592034 1.7775773 3.2107518 -0.49013516 0.23961942 -0.49137297 2.6538186 0.17805131 4.6951847 -0.8515365 0.2484263 -0.24166095 -0.49876228 -1.9606694 0.6583797 -0.29018334 0.74730545 -1.4244006 -1.4069889 0.38690162 0.3984781 0.26625094 0.7648409 0.9068775 2.2632122 -3.0596607 -1.0655171 0.44265392 2.187483 -0.75397056 -1.1137778 1.037866 1.6357373 0.30793694 1.426589 -0.0140623925 2.7699513 0.93855846 -2.74409 -1.2205495 2.7866352 0.3263284 0.361695 -0.9518102 0.29678184 -1.3184574 -1.5634623 0.5294351 0.44420967 0.8434213 -0.23158762 0.8924956 -2.944478 -1.8577719 -2.4979134 -3.0287344 -1.4789927 -0.40230796 -1.3835007 -0.24032575 -1.8170402 0.5287852 -3.3920603 2.140627 0.6495443 0.71653783 2.6088176 0.89387614 -0.6922023 0.7578225 1.9536898 0.6307929 1.4941614 2.2406754 3.2806783 1.1104231 -2.656999 -1.1762067 -1.4914 3.0589187 -2.3027747 -1.8830142 -2.6229434 3.082932 0.6852205 -3.7113485 -0.8154832 1.1278921 -0.9137234 3.2771862 -2.16644 1.3456186 -1.2308489 2.2742133 3.260759 1.714534 -0.18105167
ស -1.9436793 -0.88822883 -2.2097137 -0.50116974 -1.3968556 -0.0117184445 0.9381349 0.31583863 -1.5071626 1.0071632 -1.4867097 0.2901598 -1.1807053 -1.1956975 -1.166029 -0.82675743 -0.4644911 1.0564482 -1.3155714 1.8384495 -2.0216432 -0.20248465 0.74964714 1.1569165 -0.51600194 -0.87340206 1.566198 -0.52297556 -1.9410802 2.2464888 1.9650408 -4.108883 -0.52969134 0.76272875 0.066637084 -1.6127714 1.7612748 2.7001789 2.2723842 1.1722016 0.92081064 0.58152425 -2.4390502 -0.51454836 0.18250743 -0.052965276 -1.2072121 2.3773732 -0.37088808 1.6255277 -0.97240186 -1.804408 1.3708978 -0.15491936 -0.45333582 1.2506043 -0.47580817 -0.6311435 -1.524916 0.13921604 0.5535915 -2.1895761 2.116593 -0.8869013 0.5541844 1.4276431 0.40575907 -1.5203782 -0.3478162 -0.505752 1.6583194 -0.7011502 2.6906543 -1.8678322 -1.2732313 -0.48529974 3.1758347 0.5618266 -0.87280756 0.6614251 0.8420005 -1.8340927 0.8291211 -2.6947277 -1.8346647 -2.6009107 -0.32076976 0.6095956 -1.4310707 1.5593835 2.0841606 1.2521511 2.0048227 -3.880033 1.6330886 0.3897712 0.9667535 0.59533006 2.3373818 0.18928045
ង 1.2809987 -1.8171862 0.13061304 -0.6126153 1.3005987 2.1732266 1.7394922 -0.6844176 -0.22127311 0.51925683 -0.090321206 0.06416615 0.15145126 1.0511482 -2.3737438 -0.3234689 -0.35630345 2.4083605 1.0704726 -2.2178702 0.6914316 -0.7880927 1.7531914 0.94473076 1.0044435 0.29673135 2.5510726 -0.11667207 -0.15567403 -0.9685192 1.1598203 -0.9751476 -0.3566422 2.6191404 -2.4819148 -0.26981393 -1.9565785 -0.56965935 2.3103597 -1.6066817 0.67003006 -0.77210206 -1.103871 -1.232807 0.7356214 -1.3635819 -1.135073 -2.8321846 -1.3144592 -0.673524 1.5378232 0.83362275 -2.19301 -0.39199993 -0.4526088 -2.2736514 0.21415757 -2.0728853 -1.9392238 -4.185869 -0.7429504 -2.164496 2.144676 1.0689673 -2.220722 2.8619475 -2.6572046 -1.973184 -1.6167227 -0.6137813 -0.17403086 0.45562693 -0.011865748 4.134329 -1.9989269 -0.6651892 1.8670399 0.9989097 1.592305 2.2114947 0.90159094 -0.7574378 -0.47028366 0.73707646 -2.572877 -1.6581128 1.0598404 -2.6168394 -3.1534865 0.71646065 -1.6911294 0.4544565 -1.1725566 -1.4401898 1.4548469 1.5841241 1.3208766 -1.4627237 1.5451573 1.2131182
ម -1.9294765 -0.44518587 1.5321791 1.6116946 1.0613953 1.8350513 0.7708067 -1.7340864 -1.8529115 -0.94768786 -2.3337243 -0.9003218 1.2837491 -2.3695328 0.3540757 0.9291429 0.15728362 0.9558186 -0.49517903 -1.6582435 -0.31009609 1.2177083 -0.2007549 -2.8149285 -0.6860811 2.4614587 -0.6433605 2.852755 -1.7118548 1.0461767 -1.7722967 -0.58399093 -1.79505 1.164808 -0.71749246 -0.08701414 2.4185877 1.4662986 -0.583889 4.5335064 2.5689254 0.96778464 -0.63152176 -0.62511057 2.766784 -1.7457083 0.9923896 0.712003 2.8349743 -0.834208 -1.3024971 0.5285399 1.147756 0.20614946 -1.1309391 1.7236434 -2.3949487 0.16929793 -0.47003523 -0.31274906 1.6929309 -0.77821857 1.1041162 1.8290814 -1.1268092 3.6362162 -3.1670825 1.4688716 1.0250407 -2.2759547 0.95755315 0.20917201 2.481486 0.27429292 -4.1830683 0.47885683 1.4193677 0.8007155 2.5108194 -1.4858861 -3.4825072 -1.0717494 0.23816551 -0.704951 2.4956295 -1.463007 -1.9316974 3.1870406 1.3348138 0.51386917 1.0747427 -0.5562672 -0.41699398 -0.5737251 0.62407345 0.15535034 1.6418694 -1.7637761 2.4083781 -1.4972479
ល -2.4998333 1.3430694 -0.50771886 2.1275249 1.9879087 2.0642612 2.0218263 -1.5026473 -0.84930843 1.5981587 1.2280105 1.277481 0.57379436 -3.1392715 0.61437726 -0.3945687 -0.98871356 0.73702705 -2.3049004 0.58248 0.2689652 1.7736263 1.9055561 0.7949194 0.526271 -0.5393175 0.34214297 -0.9706538 -0.76004034 -1.3055109 1.9863883 -3.0103934 -0.0837405 3.0464861 0.96316147 1.839426 0.64162207 0.8239015 2.5010097 -1.6364236 -1.8731332 0.10439661 -0.116136506 1.1530067 -1.2729815 0.39471787 -0.83015347 0.8327079 0.31021032 1.7927915 -0.0885831 1.8709862 2.152648 -2.7655218 -0.6017364 -2.650177 -1.5628288 0.9240931 -0.18477406 -3.9791176 -1.7898954 0.21585408 1.843686 -1.2342224 -0.79297346 1.6075015 -1.5915312 0.6351932 -2.53584 -0.78898996 -3.0304358 2.1346712 0.29439104 1.166207 -1.3992594 -1.0909042 1.8427864 -0.03683035 -0.575548 0.7628986 0.59554875 -0.9660898 1.9119321 -1.2144265 0.049539518 -1.1438711 2.0795074 -1.7178763 -3.098664 -0.19962887 0.9756596 -0.82512563 3.336396 -2.9275732 2.9490433 1.877374 0.9018068 1.0399613 -0.31536356 -0.48931444
ច -3.7456465 -1.5072535 -1.011736 0.88690436 -0.5847862 0.75158095 0.16340366 1.7767435 -0.9532801 -1.4987817 -1.3975681 -1.0931684 -1.0583178 -0.5232667 0.20088755 1.3870056 1.1607078 0.33519092 -1.6564399 -0.25144693 0.16582316 -0.49295524 0.40561834 -2.771357 1.9606735 0.11203313 1.0542929 1.9641887 -1.6691928 0.04361484 1.1389827 -1.9265649 -0.93734497 3.632479 -1.5121489 1.5146691 2.559222 1.1669554 -0.10814434 2.8006475 -0.055340677 3.0873923 -1.9301671 -0.61268634 -0.32021806 0.15503971 2.381948 0.93192315 0.08309442 3.5414186 1.5313773 1.1407022 0.09000539 -1.0371289 -1.6081599 -2.0814624 -3.259196 0.00038272954 -2.213208 -1.4500586 -1.3972253 2.4350145 2.7009528 -1.0170192 -0.7307917 1.2358148 -1.7369212 -1.6041955 1.2028383 -3.2289991 2.8295472 0.9547633 -0.96830374 1.546994 -1.8224638 -0.32026055 1.3590473 0.18506029 1.6421093 1.4044868 -1.6720839 -0.49007973 1.2167158 -0.41927156 0.1657303 -3.6424816 1.0526187 -0.2772258 1.23793 0.5646698 -0.97271097 2.4456038 3.8538184 -1.4540582 1.7952322 0.56579757 0.29333466 -1.3034163 2.362371 0.5890266
```

## Testing fasttext Command Line

Installation ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool$ git clone https://github.com/facebookresearch/fastText.git
Cloning into 'fastText'...
remote: Enumerating objects: 3930, done.
remote: Counting objects: 100% (944/944), done.
remote: Compressing objects: 100% (140/140), done.
remote: Total 3930 (delta 854), reused 804 (delta 804), pack-reused 2986
Receiving objects: 100% (3930/3930), 8.24 MiB | 12.75 MiB/s, done.
Resolving deltas: 100% (2505/2505), done.
(tabpfn) yekyaw.thu@gpu:~/tool$ cd fastText/
(tabpfn) yekyaw.thu@gpu:~/tool/fastText$ make
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/args.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/autotune.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/matrix.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/dictionary.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/loss.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/productquantizer.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/densematrix.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/quantmatrix.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/vector.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/model.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/utils.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/meter.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG -c src/fasttext.cc
c++ -pthread -std=c++11 -march=native -O3 -funroll-loops -DNDEBUG args.o autotune.o matrix.o dictionary.o loss.o productquantizer.o densematrix.o quantmatrix.o vector.o model.o utils.o meter.o fasttext.o src/main.cc -o fasttext
```

call --help  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText$ ./fasttext --help
usage: fasttext <command> <args>

The commands supported by fasttext are:

  supervised              train a supervised classifier
  quantize                quantize a model to reduce the memory usage
  test                    evaluate a supervised classifier
  test-label              print labels with precision and recall scores
  predict                 predict most likely labels
  predict-prob            predict most likely labels with probabilities
  skipgram                train a skipgram model
  cbow                    train a cbow model
  print-word-vectors      print word vectors given a trained model
  print-sentence-vectors  print sentence vectors given a trained model
  print-ngrams            print ngrams given a trained model and word
  nn                      query for nearest neighbors
  analogies               query for analogies
  dump                    dump arguments,dictionary,input/output vectors

(tabpfn) yekyaw.thu@gpu:~/tool/fastText$ 
```

## Testing with Example Data  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ wget https://dl.fbaipublicfiles.com/fasttext/data/cooking.stackexchange.tar.gz && tar xvzf cooking.stackexchange.tar.gz
```

Check the data:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ ls
cooking.stackexchange.id  cooking.stackexchange.tar.gz  cooking.stackexchange.txt  readme.txt
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ head cooking.stackexchange.txt 
__label__sauce __label__cheese How much does potato starch affect a cheese sauce recipe?
__label__food-safety __label__acidity Dangerous pathogens capable of growing in acidic environments
__label__cast-iron __label__stove How do I cover up the white spots on my cast iron stove?
__label__restaurant Michelin Three Star Restaurant; but if the chef is not there
__label__knife-skills __label__dicing Without knife skills, how can I quickly and accurately dice vegetables?
__label__storage-method __label__equipment __label__bread What's the purpose of a bread box?
__label__baking __label__food-safety __label__substitutions __label__peanuts how to seperate peanut oil from roasted peanuts at home?
__label__chocolate American equivalent for British chocolate terms
__label__baking __label__oven __label__convection Fan bake vs bake
__label__sauce __label__storage-lifetime __label__acidity __label__mayonnaise Regulation and balancing of readymade packed mayonnaise and other sauces
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$
```
The whole corpus size is as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ wc cooking.stackexchange.txt
  15404  169582 1401900 cooking.stackexchange.txt
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ 
```

Split training, validation data:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ tail -n 3000 cooking.stackexchange.txt > cooking.valid
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ head -n 12404 cooking.stackexchange.txt > cooking.train
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ wc cooking.train 
  12404  136743 1129498 cooking.train
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ wc cooking.valid 
  3000  32839 272402 cooking.valid
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$
```

Training ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ time ../fasttext supervised -input cooking.train -output model_cooking
Read 0M words
Number of words:  14543
Number of labels: 735
Progress: 100.0% words/sec/thread:   51717 lr:  0.000000 avg.loss: 10.162868 ETA:   0h 0m 0s

real    0m1.805s
user    0m14.153s
sys     0m0.072s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$
```

Online testing ....  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ ../fasttext predict model_cooking.bin -
Which baking dish is best to bake a banana bread ?
__label__baking
Why not put knives in the dishwasher?
__label__food-safety
```

Testing with validation file ...  
Note: The output of fastText are the precision at one (P@1) and the recall at one (R@1).  
```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ ../fasttext test model_cooking.bin cooking.valid
N       3000
P@1     0.149
R@1     0.0643
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$
```

For this time, let's calculate the precision at five and recall at five as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ ../fasttext test model_cooking.bin cooking.valid 5
N       3000
P@5     0.0687
R@5     0.148
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ 
```

One of the fasttext facility is getting the top X labels predicted by the model.   
The following is trying to get top 3 labels ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/test$ ../fasttext predict model_cooking.bin - 3
Why not put knives in the dishwasher?
__label__food-safety __label__baking __label__bread
```

Details, refers following link:  
https://fasttext.cc/docs/en/supervised-tutorial.html  

## Khmer Polarity Classification with FastText  

### Data Preparation  

Copy the dataset ...  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ cp -r kh-final-sp /home/yekyaw.thu/tool/fastText/kh-polar
```

Create a new folder (i.e. I want to separate with Original Format and Fasttext Format)  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar$ cp -r ./kh-final-sp/baseline-keyword ./kh-final-fasttext/
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar$ cp -r ./kh-final-sp/baseline-sentence ./kh-final-fasttext/
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar$ cp -r ./kh-final-sp/exp ./kh-final-fasttext/
```

Change the Format ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ ls
no-header  test.csv  tmp  train.csv  word
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ cut -f1 -d',' ./train.csv > train.f1
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ cut -f2 -d',' ./train.csv > train.label
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ cut -f1 -d',' ./test.csv > test.f1
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ cut -f2 -d',' ./test.csv > test.label
```

Removed top header line:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed -i '1d' ./train.f1
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed -i '1d' ./train.label 
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed -i '1d' ./test.label 
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed -i '1d' ./test.f1 
```

Check/Confirm ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ wc train.f1 train.label
   9014  698067 5108408 train.f1
   9014    9014   80296 train.label
  18028  707081 5188704 total
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ wc test.f1 test.label
  1000  75892 554531 test.f1
  1000   1000   8908 test.label
  2000  76892 563439 total
```

Test for adding prefix ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed 's/^/__label__/;' ./test.label | head
__label__negative
__label__negative
__label__positive
__label__positive
__label__neutral
__label__negative
__label__positive
__label__positive
__label__positive
__label__positive
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$
```

Adding prefix to train and test label files ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed 's/^/__label__/;' ./test.label > test.label.fasttext
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ sed 's/^/__label__/;' ./train.label > train.label.fasttext
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ tail ./test.label.fasttext 
__label__positive
__label__positive
__label__negative
__label__negative
__label__positive
__label__positive
__label__negative
__label__negative
__label__positive
__label__positive
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ tail ./train.label.fasttext 
__label__positive
__label__positive
__label__negative
__label__positive
__label__positive
__label__negative
__label__negative
__label__positive
__label__positive
__label__positive
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$
```

paste text and label ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ paste -d " " ./train.label.fasttext train.f1 > train.sentence.fasttest
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ paste -d " " ./test.label.fasttext test.f1 > test.sentence.fasttest
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ head -n 3 ./train.sentence.fasttest 
__label__negative ▁រដ្ឋ ម ន្ត រី ប រ ិ ស្ថាន អ ៊ ុយ ក្រ ែន បាន បញ្ជា ក់ កាល ពី ថ ្ ង ៃ ច ន្ទ ទី ▁៣ ▁ខែ ត ុល ា ថា ▁ការ ខ ូ ច ខាត ប រ ិ ស្ថាន ក្នុង ប្រ ទេស អ ៊ ុយ ក្រ ែន ដែ ល ប ណ្តាល មក ពី ការ ឈ ្ល ាន ព ាន រ ប ស់ រ ុ ស្ ស៊ី ត្រ ូវ បាន គេ ប៉ ាន់ ប្រ មា ណ ថា ▁មាន ទ ំ ហ ំ ជា ង ▁៣ ៥ ៣ ព ាន់ ល ាន ដ ុល ្ល ារ ▁ជាមួយ នឹង ត ំ ប ន់ អ ភ ិ រ ក្ស ធ ម្ ម ជាតិ រ ាប់ ល ាន ហ ិក តា ទ ៀ ត ស្ ថ ិត ន ៅ ក ្រោម ការ គ ំ រា មក ំ ហ ែង ▁។
__label__neutral ▁ខ្ញុំ ច ង់ ច ាប់ ផ្តើម ប្រ ើ ផ ា ស ពិសេស ស ំ រ ាប់ អ ្ន ក ធ្វើដំណើរ
__label__neutral ▁ក្រោយ ពេល ដែ ល វា បាន ហ ែ ល ប ត់ ច ុះ ប ត់ ឡើង គ ្រ ប់ ៗ ក ន ្ល ែង វា ទៅ ដល់ ស្រ ុក ខ ោ ន ហើយ វា ស ំ ច ត ន ៅ ទី នោះ ២ . ២ ថ ្ ង ៃ ទ ើ ប វា ហ ែ ល ច ុះ មក វិញ ។
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ head -n 3 ./test.sentence.fasttest 
__label__negative ▁ នេះ ប ើ តា ម ប្រ សា ស ន៍ រ ប ស់ ▁ឯក ឧ ត្ត ម ▁ ន េ ត្រ ▁ភ ក ្ត រា ▁រដ្ឋ លេខ ា ធ ិ ការ ▁និង ជា អ ន ុ ប្រ ធាន អ ច ិ ន្ត រ ៃ យ ៍ ក្រ ុ ម ការ ង ារ ប្រឆាំង ការ ស ម្ អា ត ប្រ ាក់ នៃ ក្រ ស ួង ប រ ិ ស្ថាន ▁កាល ថ ្ ង ៃ ទី ៥ ▁ខែ ត ុល ា ▁ឆ្នាំ ២ ០ ២ ២ ▁។
__label__negative ▁ចំណ ែក ▁ម ន្ត រី ▁ សិទ្ធិ ម ន ុ ស្ស ▁និង ▁អ្នក វិ ភ ា គ ▁យល់ ▁ថា ▁អ្វី ▁ដែល ▁លោក ▁ ហ៊ុន ▁ស ែន ▁លើក ▁ឡើង ▁មក ▁នោះ ▁ជា ▁វ ោ ហា រ សា ស្ត រ ▁ ន យោប ាយ ▁ដើម្បី ▁ប ន ្ល ំ ▁ការ ▁ពិ ត ▁ប៉ុណ្ណ ោះ ។
__label__positive ▁ការងា រ មាន ស្ ថ ិ រ ភាព ▁ហើយ អ ្ន ក អា ច ទ ទ ួល បាន ស ម ិទ្ធ ផល ជ ាក់ ល ាក់ ក្នុង អា ជ ី ព រ ប ស់ អ ្ន ក ▁ ធាន ា ជ ី វ ិត រ ប ស់ អ ្ន ក ។
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence$ 
```

## Training Kh Polarity with FastText 

Exciting ... :)  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model1
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 1486212 lr:  0.000000 avg.loss:  0.805035 ETA:   0h 0m 0s

real    0m0.388s
user    0m1.712s
sys     0m0.063s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Check the model and vector filesize ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ wc ./kh-polar.model1.bin
   3722   20802 1058769 ./kh-polar.model1.bin
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ wc ./kh-polar.model1.vec 
   2531  255532 2603288 ./kh-polar.model1.vec
```

## Testing the FastText Model  

Testing with Validation data ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model1.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.665
R@1     0.665

real    0m0.015s
user    0m0.011s
sys     0m0.004s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Testing with precision at X and recall at X ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model1.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 4
N       1000
P@4     0.333
R@4     1

real    0m0.013s
user    0m0.013s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model1.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 3
N       1000
P@3     0.333
R@3     1

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model1.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 2
N       1000
P@2     0.457
R@2     0.914

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model1.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 5
N       1000
P@5     0.333
R@5     1

real    0m0.015s
user    0m0.015s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

## Training with More Epoch  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model2 -epoch 25
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2127158 lr:  0.000000 avg.loss:  0.674152 ETA:   0h 0m 0s

real    0m0.886s
user    0m7.702s
sys     0m0.072s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

Testing with Epoch 25 Model ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model2.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.685
R@1     0.685

real    0m0.015s
user    0m0.010s
sys     0m0.005s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

Wow! Now We reach to 68!!!   

Training with Epch 30 ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model3 -epoch 30
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2234201 lr:  0.000000 avg.loss:  0.645315 ETA:   0h 0m 0s

real    0m0.986s
user    0m9.196s
sys     0m0.072s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model3.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.683
R@1     0.683

real    0m0.015s
user    0m0.015s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Training with Epoch 35 ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model4 -epoch 35
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2316818 lr:  0.000000 avg.loss:  0.634116 ETA:   0h 0m 0s

real    0m1.090s
user    0m10.464s
sys     0m0.132s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model4.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.683
R@1     0.683

real    0m0.015s
user    0m0.015s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Training with Epoch 40 ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model5 -epoch 40
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2382689 lr:  0.000000 avg.loss:  0.618567 ETA:   0h 0m 0s

real    0m1.187s
user    0m12.051s
sys     0m0.092s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model5.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.678
R@1     0.678

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

Training with Epoch 45 ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model6 -epoch 45
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2234529 lr:  0.000000 avg.loss:  0.641646 ETA:   0h 0m 0s

real    0m1.383s
user    0m13.540s
sys     0m0.076s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model6.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.679
R@1     0.679

real    0m0.014s
user    0m0.010s
sys     0m0.004s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Training with Epoch 50 ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model7 -epoch 50
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2291591 lr:  0.000000 avg.loss:  0.597095 ETA:   0h 0m 0s

real    0m1.481s
user    0m15.027s
sys     0m0.108s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model7.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.673
R@1     0.673

real    0m0.015s
user    0m0.010s
sys     0m0.005s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Current Best Model is with Epoch 25!, got 685!!!  

## Training with Various Learning Rate

with lr 1.0  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 25 -lr 1.0
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2126836 lr:  0.000000 avg.loss:  0.646921 ETA:   0h 0m 0s

real    0m0.882s
user    0m7.579s
sys     0m0.080s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.673
R@1     0.673

real    0m0.015s
user    0m0.015s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

with lr 0.9  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 25 -lr 0.9
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2127778 lr:  0.000000 avg.loss:  0.650086 ETA:   0h 0m 0s

real    0m0.882s
user    0m7.760s
sys     0m0.084s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.683
R@1     0.683

real    0m0.014s
user    0m0.011s
sys     0m0.004s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

with -lr 0.8

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 25 -lr 0.8
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2127017 lr:  0.000000 avg.loss:  0.557731 ETA:   0h 0m 0s

real    0m0.884s
user    0m7.662s
sys     0m0.072s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.675
R@1     0.675

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

## Playing with Both No. of Epoch and LR

lr 0.8, epoch 50  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 50 -lr 0.8
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2291517 lr:  0.000000 avg.loss:  0.593896 ETA:   0h 0m 0s

real    0m1.478s
user    0m15.009s
sys     0m0.100s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.68
R@1     0.68

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 

```

lr 0.8, epoch 100  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 100 -lr 0.8
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2383831 lr:  0.000000 avg.loss:  0.587188 ETA:   0h 0m 0s

real    0m2.683s
user    0m29.755s
sys     0m0.184s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.674
R@1     0.674

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

lr 0.1, epoch 100  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 100 -lr 0.1
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2384175 lr:  0.000000 avg.loss:  0.587857 ETA:   0h 0m 0s

real    0m2.680s
user    0m29.798s
sys     0m0.176s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.675
R@1     0.675

real    0m0.014s
user    0m0.011s
sys     0m0.004s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

lr 0.9, epoch 100  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 100 -lr 0.9
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2384266 lr:  0.000000 avg.loss:  0.556359 ETA:   0h 0m 0s

real    0m2.684s
user    0m29.800s
sys     0m0.180s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.673
R@1     0.673

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

lr 1.0, epoch 100  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-dummy -epoch 100 -lr 1.0
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2383657 lr:  0.000000 avg.loss:  0.613141 ETA:   0h 0m 0s

real    0m2.690s
user    0m29.956s
sys     0m0.152s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test ./kh-polar.model-dummy.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest 
N       1000
P@1     0.669
R@1     0.669

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

## Detail Study 

Currently, as shown in above, the best model is with epoch 25 and default learning rate.   
We wanna see detail classification results ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model2 -epoch 25
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 2127158 lr:  0.000000 avg.loss:  0.674152 ETA:   0h 0m 0s

real    0m0.886s
user    0m7.702s
sys     0m0.072s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

by using "-test-label" option  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext test-label ./kh-polar.model2.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
F1-Score : 0.775081  Precision : 0.733538  Recall : 0.821612   __label__positive
F1-Score : 0.588045  Precision : 0.619048  Recall : 0.560000   __label__negative
F1-Score : 0.331034  Precision : 0.452830  Recall : 0.260870   __label__neutral
N       1000
P@1     0.685
R@1     0.685

real    0m0.015s
user    0m0.014s
sys     0m0.000s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

## Playing with Word N-gram

Training with -wordNgrams 2  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-ep25-2ngram -epoch 25 -wordNgrams 2
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 1488623 lr:  0.000000 avg.loss:  0.382440 ETA:   0h 0m 0s

real    0m2.491s
user    0m12.746s
sys     0m0.711s
```

The results increased as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep25-2ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
F1-Score : 0.809603  Precision : 0.782400  Recall : 0.838765   __label__positive
F1-Score : 0.671779  Precision : 0.669725  Recall : 0.673846   __label__negative
F1-Score : 0.342857  Precision : 0.500000  Recall : 0.260870   __label__neutral
N       1000
P@1     0.732
R@1     0.732
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Training with 3gram  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-ep25-3ngram -epoch 25 -wordNgrams 3
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 1063504 lr:  0.000000 avg.loss:  0.416603 ETA:   0h 0m 0s

real    0m2.527s
user    0m17.302s
sys     0m0.790s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Wow! The results increased!!!  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep25-3ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
F1-Score : 0.815244  Precision : 0.788462  Recall : 0.843911   __label__positive
F1-Score : 0.684848  Precision : 0.674627  Recall : 0.695385   __label__negative
F1-Score : 0.330827  Precision : 0.536585  Recall : 0.239130   __label__neutral
N       1000
P@1     0.740
R@1     0.740
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

I think, The reason is we are using sub-word unit (SentencePiece) ...  
Let's try with 4 ngram ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-ep25-4ngram -epoch 25 -wordNgrams 4
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread:  930053 lr:  0.000000 avg.loss:  0.451212 ETA:   0h 0m 0s

real    0m2.263s
user    0m20.265s
sys     0m0.420s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep25-4ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__positive
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__negative
F1-Score : 0.168498  Precision : 0.092000  Recall : 1.000000   __label__neutral
N       1000
P@1     0.092
R@1     0.092
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

Now the results are decreased ..., we might need more epoch ...  
Try with epoch 50, 4-gram ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-ep50-4ngram -epoch 50 -wordNgrams 4
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread:  930419 lr:  0.000000 avg.loss:  0.217324 ETA:   0h 0m 0s

real    0m3.822s
user    0m38.797s
sys     0m0.480s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep50-4ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__positive
F1-Score : 0.000000  Precision : --------  Recall : 0.000000   __label__negative
F1-Score : 0.168498  Precision : 0.092000  Recall : 1.000000   __label__neutral
N       1000
P@1     0.092
R@1     0.092
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

For this time, I wanna try with 3-gram and epoch 50 ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext supervised -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-ep50-3ngram -epoch 50 -wordNgrams 3
Read 0M words
Number of words:  2530
Number of labels: 3
Progress: 100.0% words/sec/thread: 1240652 lr:  0.000000 avg.loss:  0.210817 ETA:   0h 0m 0s

real    0m2.885s
user    0m29.252s
sys     0m0.336s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep50-3ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
Aborted (core dumped)
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

2gram, epoch 30 also failed ...  

## Many Prediction as Possible

Now let's have a look on our predictions, we want as many prediction as possible (argument -1) and we want only labels with probability higher or equal to 0.5 :

Until now, Best Result is as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep25-3ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
F1-Score : 0.815244  Precision : 0.788462  Recall : 0.843911   __label__positive
F1-Score : 0.684848  Precision : 0.674627  Recall : 0.695385   __label__negative
F1-Score : 0.330827  Precision : 0.536585  Recall : 0.239130   __label__neutral
N       1000
P@1     0.740
R@1     0.740
```

How about testing with the argument -1:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-ep25-3ngram.bin ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest -1
F1-Score : 0.736576  Precision : 0.583000  Recall : 1.000000   __label__positive
F1-Score : 0.490566  Precision : 0.325000  Recall : 1.000000   __label__negative
F1-Score : 0.168498  Precision : 0.092000  Recall : 1.000000   __label__neutral
N       1000
P@-1    0.333
R@-1    1.000
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ 
```

As you can see in above, Precision and Recall are not balanced. Not good! 

## Comparison between Skipgram and Cbow

Default Skipgram Failed as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext skipgram -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-skipgram
Read 0M words
Number of words:  1083
Number of labels: 3
Progress: 100.0% words/sec/thread:  248297 lr:  0.000000 avg.loss:  2.565338 ETA:   0h 0m 0s

real    0m2.691s
user    0m15.982s
sys     0m0.700s
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ ../../fasttext test-label ./kh-polar.model-skipgram. ../kh-final-fasttext/baseline-sentence/test.sentence.fasttest
Aborted (core dumped)
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$
```

Default Training/Testing with cbow also failed ...  

```
(tabpfn) yekyaw.thu@gpu:~/tool/fastText/kh-polar/model$ time ../../fasttext cbow -input ../kh-final-fasttext/baseline-sentence/train.sentence.fasttest -output kh-polar.model-cbow
Read 0M words
Number of words:  1083
Number of labels: 3
Progress: 100.0% words/sec/thread:  496142 lr:  0.000000 avg.loss:  2.602888 ETA:   0h 0m 0s

real    0m2.104s
user    0m7.875s
sys     0m0.754s
```

We need to explore more!!!   


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

## To Do

- Currently we used SentencePiece Segmentation Unit, We can try with Word Unit, and also Word2Vec etc.  
- We can also try with some more ML Classification Techniques
- To increase the size of the current Khmer Polarity Corpus

## Reference

- https://stackoverflow.com/questions/22129943/how-to-calculate-the-sentence-similarity-using-word2vec-model-of-gensim-with-pyt
- https://towardsdatascience.com/word2vec-for-phrases-learning-embeddings-for-more-than-one-word-727b6cf723cf
- https://www.analyticsvidhya.com/blog/2020/08/top-4-sentence-embedding-techniques-using-python/
- https://github.com/rmadan16/TF-IDF
- https://scikit-learn.org/stable/datasets/loading_other_datasets.html
- https://stackabuse.com/text-classification-with-python-and-scikit-learn/
- https://pypi.org/project/fasttext/
- https://github.com/bentrevett/pytorch-sentiment-analysis
- https://stackoverflow.com/questions/61768902/using-fasttext-sentence-vector-as-an-input-feature
- https://towardsdatascience.com/building-a-sentence-embedding-index-with-fasttext-and-bm25-f07e7148d240
- https://towardsdatascience.com/fasttext-under-the-hood-11efc57b2b3






