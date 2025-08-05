
# Deployment Instructions for DPUPFLDDetector

## Files
- dpupfld_detector.xmodel: Compiled model for KV260
- pfld.yaml: Model configuration
- arch.json: DPU architecture file

## Usage
1. Copy all files to KV260
2. Use the xmodel with Vitis AI Runtime
3. Input image size: 112x112
4. Number of landmarks: 196

## Performance
- Float model NME: 0.0718
- Quantized model NME: 0.0729
- NME increase: 1.51%
