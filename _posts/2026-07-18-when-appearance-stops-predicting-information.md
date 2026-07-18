---
title: "When Appearance Stops Predicting Information: My Experience of the 2026 Deep Reconstruction Workshop"
collection: posts
permalink: /year-archive/when-appearance-stops-predicting-information
excerpt: "Notes from the 2026 Deep Reconstruction Workshop at Penn Medicine's Smilow Center, on how learned image reconstruction can make images look cleaner while carrying less real information."
date: 2026-07-18
venue: "Technical Blog"
---

# When Appearance Stops Predicting Information: My Experience of the 2026 Deep Reconstruction Workshop

Imaging systems are compression pipelines with human judgment at the end. Older reconstruction methods, like filtered backprojection, were honest about information loss: you could point to where signal was thrown away. Learned reconstruction with neural networks blurs that relationship. An image can get cleaner and carry less at the same time, and nothing in the visual presentation tells you which happened.

I attended the 2026 Deep Reconstruction Workshop at Penn Medicine's Smilow Center. Three speakers presented distinct engineering approaches to this problem, and a fourth session rounded out the day with evaluation methods.

## Part I: Mitchell Schnall, The Failure Mode Is Silent

**The imaging chain**

Schnall framed clinical imaging as four stages: signal acquisition, image reconstruction, image analysis, and results communication. Machine intelligence increasingly handles both reconstruction and analysis with growing autonomy.

**Deterministic vs. probabilistic processing**

Deterministic processing applies fixed, characterizable transforms. Probabilistic editing applies learned transforms based on models of what data "should" look like. A denoiser trained on population images learns to strip out statistically improbable features. Under normal conditions that is desirable. Under anomalous conditions, improbable and pathological are the same thing.

**Economic drivers**

The shift toward learned reconstruction comes from physics constraints. CT is photon-limited, so dose reduction with maintained diagnostic performance drives adoption. MR is time-limited, so fewer k-space samples mean shorter exams and higher throughput. These gains are real and clinically valuable.

**The core hazard**

The danger isn't visibly wrong images, readers reject those. It's well-formed fabrications. Schnall described cases where displayed structures had no corresponding tissue, and bright artifacts that persisted across years of studies. The presence of a feature in the image does not establish its presence in the patient.

He argued for a regulatory model based on CLIA (Clinical Laboratory Improvement Amendments), which validates chemical analyses against defined performance characteristics. Radiology has no structural equivalent for learned image processing.

## Part II: Rene Vidal, Reconstruction With a Job to Do

**The engineering problem**

Vidal's work on lens-free holographic imaging for complete blood counts shows how algorithmic reconstruction can become the product itself. Stripping the objective lens makes hardware compact and cheap, but produces nearly uninterpretable pixelated shadows.

**The formulation**

Phase retrieval is the core problem: the sensor records only diffraction magnitude, losing phase information, which creates artifacts. The recovery objective minimizes the difference between measured and modeled intensities, but the magnitude operator makes this non-convex. Vidal noted that essentially every problem in this class is non-convex, and the craft lies in constructing formulations that stay tractable.

**Methodological progression**

Four stages incrementally strengthened priors:

1. Physically accurate angular spectrum reconstruction
2. Sparsity regularization exploiting cell distributions
3. Learned dictionary atoms encoding cell type diffraction signatures
4. Deep sparse networks with complex-valued layers preserving field structure

**Removing the annotation bottleneck**

Instead of manual per-cell labeling, Vidal's approach learns from label proportions via optimal transport, using reference hematology analyzer outputs as supervision. That removes recalibration burdens when reconstruction methods change.

The key insight: this system is validated against an established analyzer, not against a preferred image. Reconstruction quality is instrumental, never terminal.

## Part III: Web Stayman, Encode What You Already Know

**Why metal is brutal**

CT reconstruction near metal implants fails for three compounding reasons: photon starvation amplifies noise, beam hardening violates monoenergetic assumptions, and nonlinear partial-volume effects create propagating streaks.

**Known component reconstruction**

Stayman's approach jointly estimates background anatomy and known implant pose or deformation using parametric models. This enables multi-resolution decomposition, 0.4mm voxels for unknown tissue, 0.1mm for fully-specified implants. Individual electrode contacts become visible instead of lost in blur.

The principle mirrors known software symbols: if the definition already exists, spending inference capacity to rediscover it is wasted effort, and worse, it injects error where none needed to exist.

**Diffusion posterior sampling**

The move toward diffusion models trained on anatomical data provides learned priors without parametric models, relaxing the component model requirement.

**Combining priors across scales**

Multi-prior strategies that mix different resolution-scale reconstructions in the frequency domain outperform single-prior approaches, assigning each prior to the frequency bands where it is most reliable.

## Part IV: The Rest of the Day

**Angel Pineda, task-based metrics**

Full-reference metrics like SSIM compare against differently-acquired reference images and measure stylistic agreement, not task performance. Pineda argued for detection-theoretic evaluation that measures whether signal-present and signal-absent distributions actually separated.

His accelerated MRI data showed a critical gap: conventional assessment supported 5x acceleration, while task-based detection analysis defended only 3x. Conventional assessment recommends more acceleration than task-based assessment permits, and that gap is a specification error.

He also showed that networks trained on partially-sampled k-space centers develop brittle dependencies on that corruption structure. Out-of-distribution inputs without fully-sampled centers cause degradation sharper than human observers experience.

**Xiaofeng Yang, image-domain shortcuts**

Yang's low-dose PET enhancement work explicitly trades measurement-domain information for integration simplicity. Working in image domain fits existing pipelines without scanner or software changes, but sacrifices access to raw counts. Counts lost at one-eighth dose cannot be recovered, only plausibly interpolated, and the objective cannot distinguish a correct interpolation from a confident one.

## Closing Thoughts

Reconnecting with former mentors now advancing this field, Grace Gang organizing the workshop, Web Stayman's matured Known Component Reconstruction line, and Rene Vidal's commercial lens-free products, was genuinely satisfying. Watching these researchers ask the sharpest questions in the room left me with a long list of papers to read.

Read the full article on Medium:
[When Appearance Stops Predicting Information: My Experience of the 2026 Deep Reconstruction Workshop](https://medium.com/p/fa9d68a966aa)
