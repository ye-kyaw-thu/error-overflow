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
