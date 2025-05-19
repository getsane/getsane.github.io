---
layout: post
title:  "PyTensor/BLAS warning on Emacs"
date:   2025-01-18 10:27:29 -0400
categories: Emacs
---
Emacs was giving a warning 'Using NumPy C-API based implementation for BLAS functions' when executing a script that was importing `pytensor`.
I noticed that this was not the case when executing the script from the `terminal`.

The fix was the following:  
 In an interactive python session from the *terminal*, run
 {% highlight python  %}
import pytensor as pt
pt.config.blas__ldflags
{% endhighlight %}

 Since `pytensor` was working fine in the in the interactive session in ther terminal, the code produced the following output: 
`-L/Users/uname/opt/miniconda3/envs/pymc_env/lib -lmkl_core -lmkl_rt -lmkl_intel_thread -liomp5 -lpthread -Wl,-rpath,/Users/Username/opt/miniconda3/envs/pymc_env/lib`
 3. Add to `.pytensorrc` file the below lines and save this file in the $HOME folder. Remember to replace Username.

{% highlight bash %}
[blas]
ldflags=-L/Users/Username/opt/miniconda3/envs/pymc_env/lib -lmkl_core -lmkl_rt -lmkl_intel_thread -liomp5 -lpthread -Wl,- rpath,/Users/Username/opt/miniconda3/envs/pymc_env/lib
{% endhighlight %}

