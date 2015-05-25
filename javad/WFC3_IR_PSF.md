<h1 id="hst-wfc3ir-psf">HST WFC3/IR PSF</h1>

<p>We are working on building a super resolution– at resolution higher than the that of native pixel in the data– model for the pixel-convolved point spread function of <strong>WFC3/IR</strong> instrument of <strong>HST</strong>.  <br>
<script id="MathJax-Element-1" type="math/tex; mode=display">
\mathbf{y}_{ij} = f_i\sum_{l}\mathbf{X}_{l}K^{(i)}_{lj}+ \mathbf{B}_{i}+\text{noise},
</script> <br>
where the variance of the noise model is <br>
<script id="MathJax-Element-2" type="math/tex; mode=display">
\mathbf{var}_{ij} = \sigma^{2} + g\Big(f_i\sum_{l}\mathbf{X}_{l}K^{(i)}_{lj}\Big),
</script> <br>
 where the first term is variance of the a floor un-correlated Gaussian noise whose value (<script id="MathJax-Element-3" type="math/tex">\sigma^{2} \simeq 0.05</script> ) comes along with the data we are working with. The origin of the second term is the Poisson noise whose variance is computed by multiplying a gain factor (<script id="MathJax-Element-4" type="math/tex">g\simeq 0.01</script>) and the PSF model rendered at the data grid. </p>

<p>In our <script id="MathJax-Element-5" type="math/tex">\chi^{2}</script> optimization, we add a term proportional to some smoothness prior with a strength set by some hyper-parameter <script id="MathJax-Element-6" type="math/tex">\epsilon</script>. </p>

<p>An example of the model for bright stars is the following: <br>
 <img src="http://broiler.astrometry.net/~mv1003/tangy/bright.png" alt="enter image description here" title=""> <br>
 And for relatively bright stars: <br>
 <img src="http://broiler.astrometry.net/~mv1003/tangy/less_bright.png" alt="enter image description here" title=""> <br>
<img src="http://broiler.astrometry.net/~mv1003/tangy/less_bright2.png" alt="enter image description here" title=""> <br>
And faint stars: <br>
<img src="http://broiler.astrometry.net/~mv1003/tangy/faint.png" alt="enter image description here" title=""></p>

<hr>



<h2 id="todo-list">TODO list</h2>

<p>There are many parameters to tune, such as the smoothness strength, up-sampling factor, and perhaps parameters of the noise model. In order for us to be able to fully explore those options we need to speed-up the code. <br>
The Problem is highly parallelizable, but we are not taking advantage of that. Furthermore, we can use something like cython to make the likelihood evaluation even faster. <br>
In some cases, the sampling operator results in numerical artifacts– due to numerical instabilities– along the edges of each patch. We need to fix that as well! </p>