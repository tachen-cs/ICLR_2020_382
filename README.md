# Wav2Letter+ attack based on IPC 
Code for ICLR_2020 paper (under review)

**Generating Robust Audio Adversarial Examples using Iterative Proportional Clipping** <br />
**[[Paper](https://openreview.net/forum?id=HJgFW6EKvH)]** <br />

### Installation
Install PyTorch if you haven't already.

Install this fork for Warp-CTC bindings:

    $ git clone https://github.com/SeanNaren/warp-ctc.git
    $ cd warp-ctc
    $ mkdir build; cd build
    $ cmake ..
    $ make
    $ export CUDA_HOME="/usr/local/cuda"
    $ cd ../pytorch_binding
    $ python setup.py install

Install pytorch audio:

    $ sudo apt-get install sox libsox-dev libsox-fmt-all
    $ git clone https://github.com/pytorch/audio.git
    $ cd audio
    $ pip install cffi
    $ python setup.py install

If you want decoding to support beam search with an optional language model, install ctcdecode:

    $ git clone --recursive https://github.com/parlance/ctcdecode.git
    $ cd ctcdecode
    $ pip install .

Finally clone this repo and run this within the repo:

    $ pip install -r requirements.txt

### Inference 
We give two demos for researchers to reproduce our work.
1. Please download the [BaiDuYun](https://pan.baidu.com/s/1SuveHraSzv_Q9LhhOxxS4A) (code:ffgq).
2. Unzip the [4-gram.arpa.tar.gz] under the root directory, and put the [pretrained_wav2Letter.pth.tar] under the "model_libri" folder.
3. 
Run the following code to attack from original1 to target1:

    $ python attack_stage1.py --orig-path ./data/original/original1.wav --target-path ./data/target/target1.txt
    $ python attack_stage2.py --audio-path ./generated_stage1/original1_to_target1_stage1.wav --orig-path ./data/original/original1.wav --target-path ./data/target/target1.txt

Run the following code to attack from original2 to target2:

    $ python attack_stage1.py --orig-path ./data/original/original2.wav --target-path ./data/target/target2.txt
    $ python attack_stage2.py --audio-path ./generated_stage1/original2_to_target2_stage1.wav --orig-path ./data/original/original2.wav --target-path ./data/target/target2.txt 
4. the generated adversarial audios are under generated_stage2 folder.
