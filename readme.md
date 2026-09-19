# cli-benchmark

Measures how long a command-line program takes to run: repeats it a given number of times,
sequentially or in parallel, and reports timing statistics.

## Why

Timing a command once tells you almost nothing — the first run pays for cold caches, and any
single run is one sample of a noisy distribution. This script runs the command N times and
reports the spread, and it can run those N copies in parallel, which is the quickest way to see
how a program behaves when it competes with itself for cores and I/O.

## Requirements

Python 3 and nothing else — only the standard library is used. Written against 3.6.8, also run
on 3.11. Works anywhere Python does.

## Usage

```bash
python3 sptest.py [options | config.json]
```

Options and their meaning are printed by:

```bash
python3 sptest.py -h
```

A run can also be described by a JSON file, which is convenient for keeping a benchmark
reproducible:

```json
{
    "COMMAND": "find / -type d -readable",
    "seconds": 1,
    "TIMES": 8,
    "PARALLEL": "anything - value is ignored",
    "COMMENT": "For sequential runs omit the PARALLEL key entirely - see help."
}
```

`TIMES` is the number of repetitions, `seconds` the timing resolution, and the presence of the
`PARALLEL` key — not its value — switches the run from sequential to parallel.

## Licence

MIT.
