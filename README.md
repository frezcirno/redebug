# Note

1 redebug 匹配的逻辑是 exact match，只有patch中的n-gram全部都出现在源码里面才算作匹配；
所以patch里面最好只有函数内的变更，不能包含一些乱七八糟的，比如+#include之类的

2 redebug会提取patch中的‘-’行和‘ ’行作为gram；所以patch的内容要足够长，保证处理后的gram数量要大于n，不然这个patch就会被过滤掉

3 redebug识别文件类型用的libmagic，注意安装特征文件


# ReDeBug
Unpatched code clone detection tool - reimplemented version in Python.

Please refer to our [IEEE S&P research paper](http://ieeexplore.ieee.org/document/6234404) and [USENIX ;login: article](https://www.usenix.org/publications/login/december-2012-volume-37-number-6/redebug-finding-unpatched-code-clones-entire-os) for technical details.

_Note that this is a reimplemented version in Python for usability and adaptability, and different from the original faster C implementation used in IEEE S&P evaluation._

## Dependencies
- `bitarray`, `python-magic`, and `argparse` modules: `pip install bitarray python-magic argparse`
- `libmagic` package: `apt-get install libmagic-dev` on Ubuntu/Debian, `brew install libmagic` on OSX

## Usage
Please refer to the help message for options:
```
$ python redebug.py -h
usage: redebug.py [-h] [-n NUM] [-c NUM] [-v] patch_path source_path

positional arguments:
  patch_path            path to patch files (in unified diff format)
  source_path           path to source files

optional arguments:
  -h, --help            show this help message and exit
  -n NUM, --ngram NUM   use n-gram of NUM lines (default: 4)
  -c NUM, --context NUM
                        print NUM lines of context (default: 10)
  -v, --verbose         enable verbose mode (default: False)
```
