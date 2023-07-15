
[简体中文](https://github.com/RapidAI/RapidLatexOCR/blob/main/docs/README_zh.md) | English

## Rapid Latex OCR

<p align="left">
    <a href="https://huggingface.co/spaces/SWHL/RapidLatexOCR" target="_blank"><img src="https://img.shields.io/badge/%F0%9F%A4%97-Hugging Face Demo-blue"></a>
    <a href=""><img src="https://img.shields.io/badge/Python->=3.6,<3.12-aff.svg"></a>
    <a href=""><img src="https://img.shields.io/badge/OS-Linux%2C%20Win%2C%20Mac-pink.svg"></a>
    <a href="https://pypi.org/project/rapid_latex_ocr/"><img alt="PyPI" src="https://img.shields.io/pypi/v/rapid_latex_ocr"></a>
    <a href="https://semver.org/"><img alt="SemVer2.0" src="https://img.shields.io/badge/SemVer-2.0-brightgreen"></a>
    <a href="https://github.com/psf/black"><img src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
</p>


- `rapid_latex_ocr` is a tool to convert formula images to latex format.
- **The reasoning code in the repo is modified from [LaTeX-OCR](https://github.com/lukas-blecher/LaTeX-OCR), the model has all been converted to ONNX format, and the reasoning code has been simplified, Inference is faster and easier to deploy.**
- The repo only has codes based on `ONNXRuntime` or `OpenVINO` inference in onnx format, and does not contain training model codes. If you want to train your own model, please move to [LaTeX-OCR](https://github.com/lukas-blecher/LaTeX-OCR).
- If it helps you, please give a little star ⭐ or sponsor a cup of coffee (click the link in Sponsor at the top of the page)
- Welcome all friends to actively contribute to make this tool better.

### TODO
- [ ] Rewrite LaTeX-OCR GUI version based on `rapid_latex_ocr`
- [ ] Integrate other better models

### Use
1. Installation
     - Method 1: (recommended) pip install `rapid_latext_ocr` library
        ```bash
        pip install rapid_latex_ocr
        ```
        - ⚠️Note: Because the 3 models have already reached the whl package, the package is relatively large **(156M)**, please wait patiently when downloading. The situation of each part of the model:
             |model name|size|
             |---:|:---:|
             |`image_resizer.onnx`|37.1M|
             |`encoder.onnx`|84.8M|
             |`decoder.onnx`|48.5M|
     - Method 2: Source code installation
       1. Download the warehouse source code
       2. Download the model separately ([Google Drive](https://drive.google.com/drive/folders/1e8BgLk1cPQDSZjgoLgloFYMAQWLTaroQ?usp=sharing) | [Baidu Netdisk](https://pan.baidu.com/s/1rnYmmKp2HhOkYVFehUiMNg?pwd=dh72)), put it in `rapid_latex_ocr/models`.

2. Use
     - Use by python script:
         ```python
         from rapid_latex_ocr import LatexOCR

         model = LatexOCR()

         img_path = "tests/test_files/6.png"
         with open(img_path, "rb") as f:
             data = f. read()

         result, elapse = model(data)

         print(result)
         # {\frac{x^{2}}{a^{2}}}-{\frac{y^{2}}{b^{2}}}=1

         print(elapse)
         # 0.4131628000000003
         ```
     - Use by command line:
         ```bash
         $ rapid_latex_ocr -h
         usage: rapid_latex_ocr [-h] img_path

         positional arguments:
         img_path Only img path of the formula.

         optional arguments:
         -h, --help show this help message and exit

         $ rapid_latex_ocr tests/test_files/6.png
         # ('{\\frac{x^{2}}{a^{2}}}-{\\frac{y^{2}}{b^{2}}}=1', 0.47902780000000034)
         ```
3. Input and output instructions
    - **Input(`Union[str, Path, bytes]`)**: An image containing only formulas.
    - **Output(`Tuple[str, float]`)**: `(recognition result, time-consuming)`, see the following example for details:
        ```python
        (
           '{\\frac{x^{2}}{a^{2}}}-{\\frac{y^{2}}{b^{2}}}=1',
           0.47902780000000034
        )
        ```

### ChangLog
- 2023-07-15 v0.0.1 update:
   - First release