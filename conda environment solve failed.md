#### 问题

```
lmh@ubun:~/LatentDiffusion/latent-diffusion$ conda env create -f environment.yaml
Solving environment: failed

CondaValueError: Malformed version string '~': invalid character(s).
```

#### 解决方法
```
# 1. 修改文件.condarc , 文件的目录可以通过 `conda info`找到
lmh@ubun:~/LatentDiffusion/latent-diffusion$ vim /home/lmh/.condarc

# 2. 删除（注释掉）.condarc中的 `- conda-forge`
# .condarc现在的内容

channels:
  - nvidia
#  - conda-forge
  - defaults

```

reference: 
[issue](https://github.com/conda/conda/issues/10618) 解答from @rporotti
