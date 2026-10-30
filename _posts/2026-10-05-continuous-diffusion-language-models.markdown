---
layout: research-post
title: "Continuous Diffusion Language Models"
subtitle: "A lightweight template for explaining how noising, denoising, and generation can move through continuous token spaces."
date: 2026-10-05 09:00:00 +0200
categories: research generative-modeling language-models
status: "Draft template"
published: false
reading_time: "12 minute read"
topic: "Continuous diffusion"
---

<section class="research-lede" markdown="1">
Continuous diffusion language models replace discrete token transitions with trajectories through a continuous representation space. This template is structured for a research blog post that introduces the motivation, explains the method visually, and gives readers a few small interactive handles for building intuition ([Sohl-Dickstein et al., 2015](#sohlDickstein2015deep); [Ho et al., 2020](#ho2020denoising)).

Use this opening section for the core promise of the post: what problem the work addresses, what the proposed idea changes, and why a reader interested in language models should care.
</section>

<nav class="research-toc" aria-label="Post sections">
  <a href="#motivation">Motivation</a>
  <a href="#background">Background</a>
  <a href="#method">Method</a>
  <a href="#intuition">Intuition</a>
  <a href="#experiments">Experiments</a>
  <a href="#limitations">Limitations</a>
  <a href="#links">Links</a>
</nav>

<section id="motivation" markdown="1">
## Motivation

Discrete language models are extraordinarily capable, but their generation process is usually tied to token-by-token sampling. Continuous diffusion language models offer a different design point: model a path from noise to language-like representations, then decode or project the result back into text ([Austin et al., 2021](#austin2021structured); [Li et al., 2022](#li2022diffusionlm)).

Placeholder prompts for this section:

- What bottleneck or capability gap motivates a continuous formulation?
- What should the reader understand about speed, controllability, or parallel generation?
- Which examples make the motivation concrete without requiring heavy notation?
</section>

<section class="research-demo diffusion-demo" aria-labelledby="trajectory-title">
  <div class="demo-copy">
    <p class="section-kicker">Interactive intuition</p>
    <h2 id="trajectory-title">Noising and Denoising Trajectory</h2>
    <p>Move the slider to scrub through a stylized diffusion path. Early positions are language-like; later positions are increasingly noisy. A model learns the reverse direction: recovering structure from a continuous state.</p>
    <label class="demo-slider-label" for="diffusion-step">
      <span>Diffusion time</span>
      <output id="diffusion-time" for="diffusion-step">0.42</output>
    </label>
    <input id="diffusion-step" class="demo-slider" type="range" min="0" max="100" value="42">
  </div>
  <div class="trajectory-panel" aria-hidden="true">
    <div class="trajectory-cloud" data-diffusion-cloud>
      <span style="--x: 9%; --y: 42%; --d: 0.0;"></span>
      <span style="--x: 21%; --y: 30%; --d: 0.1;"></span>
      <span style="--x: 34%; --y: 53%; --d: 0.2;"></span>
      <span style="--x: 47%; --y: 34%; --d: 0.3;"></span>
      <span style="--x: 59%; --y: 61%; --d: 0.4;"></span>
      <span style="--x: 72%; --y: 38%; --d: 0.5;"></span>
      <span style="--x: 87%; --y: 50%; --d: 0.6;"></span>
    </div>
    <ol class="token-strip" data-token-strip>
      <li>continuous</li>
      <li>diffusion</li>
      <li>models</li>
      <li>trace</li>
      <li>language</li>
    </ol>
  </div>
</section>

<section id="background" markdown="1">
## Background

Use this section to establish the minimum context: denoising diffusion, masked or discrete diffusion, continuous embeddings, and the decoding bridge from vectors back to tokens. Keep it reader-friendly by introducing one concept at a time.

Suggested ingredients:

- A brief comparison between autoregressive generation and diffusion-style generation.
- The role of token embeddings and why a continuous space is useful.
- A small note on training objectives, time conditioning, and denoising networks.
</section>

<section id="method" markdown="1">
## Method

Describe the proposed method as a sequence of choices. For example: choose a continuous representation, define a forward noising process, train a network to predict clean structure or velocity, then decode the final representation into text.

This is a good place for a compact equation, once the final notation is settled:

\\[
x_t = \alpha(t) x_0 + \sigma(t) \epsilon, \qquad \epsilon \sim \mathcal{N}(0, I)
\\]

Replace this placeholder with the paper's actual formulation, sampling procedure, and any implementation details that matter for reproducing the result.
</section>

<section class="research-demo embedding-demo" aria-labelledby="embedding-title">
  <div class="demo-copy">
    <p class="section-kicker">Embedding view</p>
    <h2 id="embedding-title">Slider-Controlled Token Interpolation</h2>
    <p>This toy view interpolates between semantic anchors. It is not a model output; it is a compact visual metaphor for continuous language representations moving between token neighborhoods.</p>
    <label class="demo-slider-label" for="interpolation-step">
      <span>Interpolation</span>
      <output id="interpolation-value" for="interpolation-step">0.55</output>
    </label>
    <input id="interpolation-step" class="demo-slider" type="range" min="0" max="100" value="55">
  </div>
  <div class="embedding-panel" aria-hidden="true">
    <div class="embedding-space">
      <span class="anchor anchor-left">syntax</span>
      <span class="anchor anchor-right">meaning</span>
      <span class="anchor anchor-mid" data-embedding-point>representation</span>
    </div>
    <div class="embedding-bars" data-embedding-bars>
      <span style="--h: 44%;"></span>
      <span style="--h: 68%;"></span>
      <span style="--h: 38%;"></span>
      <span style="--h: 76%;"></span>
      <span style="--h: 52%;"></span>
      <span style="--h: 61%;"></span>
    </div>
  </div>
</section>

<section id="intuition" markdown="1">
## Intuition

Use this section to make the method feel inevitable. A useful framing is: language has discrete symbols, but the model can still reason through smooth latent movement before committing to tokens.

Questions to answer here:

- What does "continuous" buy us conceptually?
- Where does discreteness re-enter the system?
- How should readers interpret trajectories, interpolation, or denoising steps?
</section>

<section id="experiments" markdown="1">
## Experiments

Summarize the empirical story with a clear table or figure once results are ready. Keep the first paragraph focused on the experimental question, then list datasets, baselines, metrics, and ablations.

Placeholder result themes:

- Generation quality versus number of sampling steps.
- Latency or throughput under parallel decoding.
- Controllability, infilling, or editing behavior.
- Ablations over representation space, noise schedule, and decoder.
</section>

<section id="limitations" markdown="1">
## Limitations

Be explicit about where the approach is not yet settled. Possible limitations include decoding errors, mismatch between embedding geometry and token semantics, compute costs during training, or evaluation difficulty when comparing against autoregressive baselines.

This section should be candid and specific. It is often the part that makes a research blog feel trustworthy.
</section>

<section id="links" class="research-links" markdown="1">
## Paper and Code

- Paper: [add paper link](#)
- Code: [add repository link](#)
- BibTeX: [add citation block or link](#)
</section>

<section id="references" class="research-references" markdown="1">
## References

<p id="sohlDickstein2015deep">Sohl-Dickstein, J., Weiss, E. A., Maheswaranathan, N., &amp; Ganguli, S. (2015). Deep Unsupervised Learning Using Nonequilibrium Thermodynamics. <em>Proceedings of the 32nd International Conference on Machine Learning.</em></p>

<p id="ho2020denoising">Ho, J., Jain, A., &amp; Abbeel, P. (2020). Denoising Diffusion Probabilistic Models. <em>Advances in Neural Information Processing Systems.</em></p>

<p id="austin2021structured">Austin, J., Johnson, D. D., Ho, J., Tarlow, D., &amp; van den Berg, R. (2021). Structured Denoising Diffusion Models in Discrete State-Spaces. <em>Advances in Neural Information Processing Systems.</em></p>

<p id="li2022diffusionlm">Li, X. L., Thickstun, J., Gulrajani, I., Liang, P., &amp; Hashimoto, T. B. (2022). Diffusion-LM Improves Controllable Text Generation. <em>Advances in Neural Information Processing Systems.</em></p>
</section>

<script>
  (function () {
    var diffusionSlider = document.getElementById("diffusion-step");
    var diffusionOutput = document.getElementById("diffusion-time");
    var cloud = document.querySelector("[data-diffusion-cloud]");
    var tokenStrip = document.querySelector("[data-token-strip]");
    var interpolationSlider = document.getElementById("interpolation-step");
    var interpolationOutput = document.getElementById("interpolation-value");
    var embeddingPoint = document.querySelector("[data-embedding-point]");
    var bars = document.querySelector("[data-embedding-bars]");

    function setDiffusion() {
      var t = Number(diffusionSlider.value) / 100;
      diffusionOutput.textContent = t.toFixed(2);
      cloud.style.setProperty("--t", t.toFixed(2));
      tokenStrip.style.setProperty("--blur", (t * 6).toFixed(2) + "px");
      tokenStrip.style.setProperty("--fade", (1 - t * 0.42).toFixed(2));
    }

    function setInterpolation() {
      var t = Number(interpolationSlider.value) / 100;
      interpolationOutput.textContent = t.toFixed(2);
      embeddingPoint.style.setProperty("--mix", (12 + t * 70).toFixed(1) + "%");
      bars.style.setProperty("--shift", t.toFixed(2));
    }

    if (diffusionSlider && interpolationSlider) {
      diffusionSlider.addEventListener("input", setDiffusion);
      interpolationSlider.addEventListener("input", setInterpolation);
      setDiffusion();
      setInterpolation();
    }
  })();
</script>
