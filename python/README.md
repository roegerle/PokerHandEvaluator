# PH Evaluator Python package (phevaluator)
[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/HenryRLee/PokerHandEvaluator/CI?color=green&logo=github)](https://github.com/HenryRLee/PokerHandEvaluator/actions/workflows/ci.yml)
[![PyPI version](https://badge.fury.io/py/phevaluator.svg)](https://badge.fury.io/py/phevaluator)
[![PyPI downloads](https://img.shields.io/pypi/dm/phevaluator)](https://shields.io/category/downloads)
[![Apache_2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://github.com/HenryRLee/PokerHandEvaluator/blob/master/python/LICENSE)

## Description

[PH Evaluator](https://github.com/HenryRLee/PokerHandEvaluator) is designed
for evaluating poker hands with more than 5 cards. Instead of traversing all
the combinations, it uses a perfect hash algorithm to get the hand strength
from a pre-computed hash table, which only costs very few CPU cycles and
considerably small memory (~100kb for the 7 card evaluation). With slight
modification, the same algorithm can be also applied to evaluating Omaha
poker hands.

## Installation
The library requires Python 3.
- from release on PyPI
    ```shell
    pip install phevaluator
    ```
- from source code
    ```shell
    pip install .
    ```

## Using the library
The main function is the `evaluate_cards` function.
```python
from phevaluator.evaluator import evaluate_cards

p1 = evaluate_cards("9c", "4c", "4s", "9d", "4h", "Qc", "6c")
p2 = evaluate_cards("9c", "4c", "4s", "9d", "4h", "2c", "9h")

# Player 2 has a stronger hand
print(f"The rank of the hand in player 1 is {p1}") # 292
print(f"The rank of the hand in player 2 is {p2}") # 236
```
The function can take both numbers and card strings (with a format like: 'Ah' or '2C'). Usage examples can be seen in `examples.py`.

## Test
- The pre-calculated tables (`phevaluator.tables`) are tested by comparing them with the tables generated by test codes.
- The functionality of the evaluators is tested by comparing with the JSON files generated by the original C++ evaluator.
- The functionality of the other modules is tested by its purposes.

```shell
python3 -m unittest discover -v
```

## Development
- install from source code with `editable mode`
    ```shell
    pip install -e .
    ```
    The installed package reflects changes to files inside the `phevaluator` folder automatically.

- recommended to format with [`black`](https://github.com/psf/black) before commit

    check where to correct (without formatting)
    ```shell
    black . --diff --color
    ```
    format all
    ```shell
    black .
    ```

