---
library_name: transformers
tags: []
---

## THIS PROTEIN VEC ADAPTATION WAS MODIFIED FROM https://github.com/tymor22/protein-vec

All credit for the original work goes to Tymor Hamamsy and the following authors of this paper https://www.biorxiv.org/content/10.1101/2023.11.26.568742v1

We have added a Huggingface compatible wrapper for the model in protvec.py

Please consider liking the model page and starring the github repo if you are going to use it :)

```
https://huggingface.co/lhallee/ProteinVec
https://github.com/lhallee/ProteinVecHuggingface
```

Clone and install
```
git clone https://github.com/lhallee/ProteinVecHuggingface.git
pip install torch pytorch_lightning transformers
```

To use from hugggingface
```
from transformers import T5Tokenizer
from protvec import ProteinVec, ProteinVecConfig

tokenizer = T5Tokenizer.from_pretrained('lhallee/ProteinVec')
model = ProteinVec.from_pretrained('lhallee/ProteinVec', config=ProteinVecConfig())
```

Embed a single sequence with ```embed```
```
model.to_eval()
model = model.cuda() # remove if cpu inference
embedding = model.embed('SEQWENCE').detach().cpu() # torch.tensor(1, 512)
```

Use a particular AspectVec by setting the ```inference_mask```
```
model.aspect_to_keys_dict # dictionary showing the aspects
### The model is set to ALL by default to use full ProteinVec
model.inference_mask = model.get_mask('EC') # for Enzyme Comission AspectVec
embedding = model.embed(...)
```

To half precision weights
```
model.to_half()
```


## The license for the protein vec code

### BSD 3-Clause License

Copyright (c) 2023, Tymor Hamamsy

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived from
   this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
