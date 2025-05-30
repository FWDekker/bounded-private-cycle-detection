# Finding Short Cycles in Private Networks

This is the code I used to test the algorithm as described in my thesis[^1].
Paper is WIP.

## Testing Data

The main data for testing was generated using the Barabási–Albert model[^2].
The raw data used for some of the testing was taken from a synthetic data set from IBM[^3][^4].
To start, we drop every column besides the source and target accounts.
We then factorise the account values in the dataset to integers instead of hexadecimal account numbers.
After this, we filter the graph to remove duplicate edges and self-loops.

## User instructions

### Requirements

To run the experiments, ensure you have [CMake](https://cmake.org/), [GNU Make](https://www.gnu.org/software/make/), and [GCC](https://gcc.gnu.org/) version 8 or newer installed.
On Linux systems that use `apt` (e.g. Debian, Ubuntu), you can install these programs with

```shell
sudo apt install -y cmake make gcc
```

To plot the experiments, ensure you have [Python](https://www.python.org/) version 3.10 or newer installed.
You can then install the Python packages with

```shell
pip install .
```

As usual for Python, it is recommended that you do so inside a [virtualenv](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments).

### Usage

To compile and run the experiments, execute the commands

```shell
cmake .
make
./cycle_detection_experiments
```

Results are written to the directory `out/`.
Each time you re-run the experiments, a separate log file is written to `out/`.

To plot the results contained in `<filename.log>`, run (inside your virtualenv, if you created one)
```shell
cd src/
python3 -m plotcreator <filename.log>
```

To automatically select the most recent file in `out/`, run (inside your virtualenv, if you created one)
```shell
cd src/
python3 -m plotcreator "$(find ../out/ -type f -printf "%T@ %p\n" | sort -n | cut -d' ' -f 2- | tail -n 1)"
```

Figures are stored in `out/fig/`.



[^1]: J. Jense, *Finding Bounded-Length Cycles in Decentralised Networks under Privacy Constraints*, M.Sc. thesis, Faculty of Electrical Engineering, Mathematics and Computer Science, Delft University of Technology, Delft, Netherlands, 2024. [Online](https://resolver.tudelft.nl/uuid:a559439a-d5ee-4f1f-9823-2bab3905c0c9)

[^2]: R. Albert and A.-L. Barabási, "Statistical mechanics of complex networks," *Reviews of Modern Physics*, vol. 74, no. 1, pp. 47–97, 2002. doi: [10.1103/RevModPhys.74.47](https://doi.org/10.1103/RevModPhys.74.47)

[^3]: E. Altman, J. Blanusa, L. Von Niederhäusern, B. Egressy, A. S. Anghel, and K. Atasu, *IBM Transactions for Anti Money Laundering (AML)*, Kaggle, 2023. [Online](https://www.kaggle.com/datasets/ealtman2019/ibm-transactions-for-anti-money-laundering-aml)

[^4]: E. Altman, J. Blanusa, L. Von Niederhäusern, B. Egressy, A. S. Anghel, and K. Atasu, "Realistic Synthetic Financial Transactions for Anti-Money Laundering Models," *arXiv preprint arXiv:2306.16424*, Jan. 2024. [Online](https://arxiv.org/abs/2306.16424)
