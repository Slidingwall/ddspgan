# ddspgan
ddspgan weights distilled from [pc-nsf-hifigan](https://github.com/openvpi/vocoders/releases/tag/pc-nsf-hifigan-44.1k-hop512-128bin-2025.02).

Please note that although this model is pitch-controllable, it is different from [pc-ddsp](https://github.com/yxlllc/pc-ddsp).

This model is based on [ddspgan](https://github.com/openvpi/SingingVocoders/blob/main/configs%2Fbase_ddspgan.yaml), and the discriminator uses the weights of pc-nsf-hifigan. If you want to use this model, please refer to the original repositories.

This is a personal experimental project, trained for 75,000 steps on a laptop with only a small number of audio samples. Although there is no audible difference between the model's output and that of the original pc-nsf-hifigan model when pitch remains unchanged, I still recommend comparing or fine-tuning before deployment.

Although this model is much faster than pc-nsf-hifigan in PyTorch (ddspgan / pc-nsf-hifigan: **36.38ms** / 539.10ms on CPU, **16.13ms** / 30.21ms on GPU), the exported ONNX model actually performs worse due to ONNX's poor FFT support (**1069.49ms** / 795.51ms on CPU, **981.98ms** / 64.25ms on GPU). Moreover, caching the DFT matrix increases the model size from 1.16MB to 97MB with little speedup, which somewhat defeats the purpose of distillation. Therefore, this repository only provides weights in PyTorch format.  

Training samples are randomly picked from: [Amaboshi Cipher](https://parapluie2c56m.wixsite.com/mysite/voicebank), [Children's Song Dataset](https://zenodo.org/records/4916302), [ENUNU Kodoku Project](https://github.com/oatsu-gh/enunu_kodoku_singing), [JSUT](https://sites.google.com/site/shinnosuketakamichi/publication/jsut), [Nit070](https://drive.google.com/file/d/1eFYk4HO8JzzkFYpBIzzW7WKsHNFXW-Nh/view), [NUS-48E](https://zenodo.org/records/19595152) and [Opencpop](https://wenet-e2e.github.io/opencpop/download/). Not all of these datasets necessarily contributed audio to the distillation, so I have listed all datasets in my dataset folder.  