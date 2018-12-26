#error -- unsupported GNU version! gcc versions later than 6 are not supported! chainer

=========

#if __GNUC__ > 6

//#error -- unsupported GNU version! gcc versions later than 6 are not supported!

#endif /* __GNUC__ > 6 */

========

$ pip install cupy
Collecting cupy
  Using cached https://files.pythonhosted.org/packages/1c/16/788a9e55c92a9c6b022811a30aeee9f26eef7010516d12df5a33be69484c/cupy-5.1.0.tar.gz
Requirement already satisfied: numpy>=1.9.0 in /home/yekyawthu/miniconda3/lib/python3.7/site-packages (from cupy) (1.15.4)
Requirement already satisfied: six>=1.9.0 in /home/yekyawthu/miniconda3/lib/python3.7/site-packages (from cupy) (1.11.0)
Requirement already satisfied: fastrlock>=0.3 in /home/yekyawthu/miniconda3/lib/python3.7/site-packages (from cupy) (0.4)
Building wheels for collected packages: cupy
  Running setup.py bdist_wheel for cupy ... done
  Stored in directory: /home/yekyawthu/.cache/pip/wheels/dd/c8/51/edc389a17a790b3d15b8f756f91dcbc021ce2eeb494e406a55
Successfully built cupy
Installing collected packages: cupy
Successfully installed cupy-5.1.0
(base) yekyawthu@bit-MS-7B09:~/exp/cha
