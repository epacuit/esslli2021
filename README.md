
# Probabilistic Methods in Social Choice (ESSLLI 2021)

README.md for the code used in the course [Probabilistic Methods in Social Choice](https://pacuit.org/esslli2021/prob-social-choice/).  

## Where to start

tl;dr: An overview of Profiles and voting methods is found in 01-Profiles.ipynb and 02-VotingMethods.ipynb.    

1. 01-Profiles.ipynb: Contains an overview of how to create profiles (implemented in voting/profiles.py) and generate profiles with different numbers of candidates/voters (implemented in voting/generate_profiles.py).   

A profile is created by initializing a Profile class object.  This needs a list of rankings (each ranking is a tuple of numbers), the number of candidates and a list giving the number of each ranking in the profile:

```python
from voting.profiles import Profile

rankings = [(0, 1, 2, 3), (2, 3, 1, 0), (3, 1, 2, 0), (1, 2, 0, 3), (1, 3, 2, 0)]
num_cands = 4
rcounts = [5, 3, 2, 4, 3]

prof = Profile(rankings, num_cands, rcounts=rcounts)
```

The function generate_profile is used to generate a profile for a given number of candidates and voters:  
```python
from voting.generate_profiles import generate_profile

# generate a profile using the Impartial Culture probability model
prof = generate_profile(3, 4) # prof is a Profile object with 3 candidate and 4 voters

# generate a profile using the Impartial Anonymous Culture probability model
prof = generate_profile(3, 4, probmod = "IAC") # prof is a Profile object with 3 candidate and 4 voters
```

3. Import and use voting methods (see voting/voting_methods.py for implementations and 02-VotingMethods.ipynb for an overview): 

```python
from voting.profiles import Profile
from voting.voting_methods import *

prof = Profile(rankings, num_cands, rcounts=rcounts)
print(f"The {borda.name} winners are {borda(prof)}")
```
4. See GeneratingPreferenceProfiles.ipynb for an introduction to the code to generate preference (from [preflib.org](https://preflib.org).  




## Dev Notes

* All of the code assumes that voters submit linear orders over the set of candidates. 
* In order to optimize some of the code for reasoning about profiles, it is assumed that in any profile the candidates are named by the initial segment of the non-negative integers.  So, in a profile with 5 candidates, the candidate names are "0, 1, 2, 3, and 4".   Use the `cmap` variable for different candidate names: `cmap` is a dictionary with keys 0, 1, ..., num_cands - 1 and values the "real" names of the candidates.  

<!-- #region -->
## Other Files/Directories

1. voting/profiles.py: Implementation of the Profile class used to create and reason about profile (see Profile.ipynb for an overview).

2. voting/voting_methods.py: Implementations of the voting methods (see VotingMethods.ipynb for an overview).

3. voting/generate_profiles.py: Implementation of  the function `generate_profile` to interface with the Preflib tools to generate profiles according to different probability models. 


## Requirements

All the code is written in Python 3. 

- [Preflib tools](https://github.com/PrefLib/PrefLib-Tools) (available in the voting/preflibtools directory)
- The notebooks and most of the library is built around a full SciPy stack: [MatPlotLib](https://matplotlib.org/), [Numpy](https://numpy.org/), [Pandas](https://pandas.pydata.org/)
- [numba](http://numba.pydata.org/) 
- [networkx](https://networkx.org/)
- [tabulate](https://github.com/astanin/python-tabulate)
- [seaborn](https://seaborn.pydata.org/)  
- [multiprocess](https://pypi.org/project/multiprocess/) (**only needed if simulations that use multiprocessing**) 
- [tqdm.notebook](https://github.com/tqdm/tqdm)
<!-- #endregion -->
