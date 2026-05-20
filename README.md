# UWF-FM

**Official repository of UWF-FM: Masked autoencoder-based foundation model for ultra-widefield fundus images**

UWF-FM is a foundation model pretrained on ultra-widefield fundus (UWF) images using a masked autoencoder (MAE)-based self-supervised learning framework.  
The model is designed to provide transferable visual representations for downstream UWF image analysis tasks.

> The original article will be updated soon.

---

## Overview

Ultra-widefield fundus photography captures a wide retinal field of view and provides important information about peripheral retinal lesions. However, most deep learning models for UWF images rely on supervised learning and require large labeled datasets.

UWF-FM was developed to address this limitation by pretraining a vision transformer model on a large-scale unlabeled UWF image dataset using masked image reconstruction. The pretrained encoder can then be fine-tuned for downstream UWF tasks, including retinal disease classification and image quality assessment.

---

## Model

UWF-FM follows a masked autoencoder-based pretraining strategy.

- Architecture: Vision Transformer-based masked autoencoder
- Pretraining image modality: Ultra-widefield fundus images
- Pretraining dataset: >240,000 unlabeled UWF images
- Pretraining task: Reconstruction of randomly masked retinal images
- Downstream use: Encoder fine-tuning for classification tasks

The implementation follows the MAE-based retinal foundation model framework used in RETFound, with UWF-specific pretraining.

---

## Pretrained Weights

This repository provides the pretrained UWF-FM weight.

| Model | Description | Download |
|---|---|---|
| UWF-FM | MAE-based foundation model pretrained on ultra-widefield fundus images | [Google Drive](https://drive.google.com/file/d/1eRxze51JSE7WV99gFD-Tvi_gMTEDCqWj/view?usp=drive_link) |

After downloading the checkpoint, place it in the checkpoint directory of the RETFound_MAE codebase, for example:

```bash
checkpoints/
└── UWF-FM_weight_final.pth
```

---

## Usage

This repository provides the pretrained UWF-FM weight only.  
For fine-tuning and evaluation, please use the RETFound_MAE codebase and replace the pretrained checkpoint with the UWF-FM checkpoint.

First, clone the RETFound_MAE codebase:

```bash
git clone https://github.com/rmaphoh/RETFound_MAE.git
cd RETFound_MAE
```

Then set up the environment following the instructions in the RETFound_MAE repository.

After that, download the UWF-FM pretrained weight from the link above and place it in the checkpoint directory:

```bash
checkpoints/
└── UWF-FM_weight_final.pth
```

You can then fine-tune the model using the RETFound_MAE fine-tuning pipeline by replacing the RETFound pretrained checkpoint path with the UWF-FM checkpoint path.

Example:

```bash
python main_finetune.py \
    --model vit_large_patch16 \
    --finetune checkpoints/UWF-FM_weight_final.pth \
    --data_path data/ \
    --nb_classes 3 \
    --batch_size 32 \
    --epochs 50 \
    --blr 5e-4 \
    --layer_decay 0.65 \
    --weight_decay 0.05 \
    --drop_path 0.2 \
    --input_size 224 \
    --task UWF-FM_finetune
```

Please modify `--nb_classes`, `--data_path`, and other arguments according to your dataset and task.

---

## Dataset Structure for Fine-tuning

Prepare your dataset in the format required by RETFound_MAE.  
A typical folder structure is as follows:

```bash
data/
├── train/
│   ├── class_1/
│   ├── class_2/
│   └── class_3/
├── val/
│   ├── class_1/
│   ├── class_2/
│   └── class_3/
└── test/
    ├── class_1/
    ├── class_2/
    └── class_3/
```

Each class folder should contain UWF fundus images belonging to that category.

---

## Citation

If you use UWF-FM in your research, please cite our article:

```bibtex
@article{oh2026uwffm,
  title   = {UWF-FM: Masked autoencoder-based foundation model for ultra-widefield fundus images},
  author  = {Oh, Richul and others},
  journal = {To be updated},
  year    = {2026}
}
```

Please also cite RETFound if you use the RETFound_MAE codebase:

```bibtex
@article{zhou2023foundation,
  title={A foundation model for generalizable disease detection from retinal images},
  author={Zhou, Yukun and Chia, Mark A and Wagner, Siegfried K and Ayhan, Murat S and Williamson, Dominic J and Liu, Timing and Xu, Moucheng and Lozano, Mateo G and Woodward-Court, Peter and others},
  journal={Nature},
  volume={622},
  number={7981},
  pages={156--163},
  year={2023},
  publisher={Nature Publishing Group UK London}
}
```

---

## Acknowledgements

This model was developed based on the RETFound/MAE framework.  
We thank the authors of RETFound for releasing their code and pretrained retinal foundation models.

- RETFound_MAE: https://github.com/rmaphoh/RETFound_MAE

---

## License

The license will be updated soon.

---

## Contact

For questions or collaborations, please contact:

**Richul Oh**  
Seoul National University Hospital  
Email: rcoh91@gmail.com
