This is the code used for the uncertainty experiments in the paper ["Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning"](http://mlg.eng.cam.ac.uk/yarin/publications.html#Gal2015Dropout). This code is based on the code by José Miguel Hernández-Lobato used for his paper "Probabilistic Backpropagation for Scalable Learning of Bayesian Neural Networks". The datasets supplied here are taken from the UCI machine learning repository. Note the data splits used in these experiments (which are identical to the ones used in Hernández-Lobato's code). Because of the small size of the data, if you split the data yourself you will most likely get different results to the ones here.

These experiments use Spearmint, obtained from here: [https://github.com/JasperSnoek/spearmint/tree/master/spearmint/bin](https://github.com/JasperSnoek/spearmint/tree/master/spearmint/bin).
To run an experiment:

```
./cleanup path-to-exp
THEANO_FLAGS='allow_gc=False,device=gpu,floatX=float32' ./spearmint path-to-exp/config.pb --driver=local --method=GPEIOptChooser --max-concurrent=1 --max-finished-jobs=30
```
then:
```
THEANO_FLAGS='allow_gc=False,device=gpu,floatX=float32' python experiment.py
```

I updated the scripts to run with the latest version of Keras. I also added a new experiments, using 10x training epochs compared to the original paper (which gives a drastic improvement both in terms of RMSE and test log-likelihood).

Updated results (compared to original results):

**Dataset** | Dropout RMSE (original) | Dropout Test LL (original) | Dropout RMSE (updated) | Dropout Test LL (updated)
--- | :---: | :---: | :---: | :---:
Boston Housing      | 2.97 ± 0.85 | 2.80 ± 0.84 | -2.46 ± 0.25 | -2.39 ± 0.20
Concrete Strength   | 5.23 ± 0.53 | 4.81 ± 0.64 | -3.04 ± 0.09 | -2.94 ± 0.10
Energy Efficiency   | 1.66 ± 0.19 | 1.09 ± 0.21 | -1.99 ± 0.09 | -1.72 ± 0.07
