---
layout: page
title: NumAlg
eyebrow: Numerical algorithms, for fun
permalink: /numalg/
---

A small, growing collection of numerical algorithms I've implemented outside of my PhD work — mostly classic problems in mechanics and geometry that are a good excuse to try out a time integrator or a discretization I haven't used before. Click a card to read the write-up.

<div class="card-grid">

  <a class="project-card" href="{{ "/numalg/three-body-problem/" | relative_url }}">
    <div class="project-card__media project-card__media--single">
      <img src="{{ "/assets/numalg/three-body-sketch.svg" | relative_url }}" alt="Sketch of the figure-eight three-body orbit" loading="lazy">
    </div>
    <div class="project-card__body">
      <h3>A restricted fantasy</h3>
      <p>The origin of chaos and how to get a handle on it.</p>
      <div class="project-card__tags">
        <span class="tag">ODE integrators</span>
        <span class="tag">Celestial mechanics</span>
      </div>
    </div>
  </a>

  <a class="project-card" href="{{ "/numalg/gravitational-waves/" | relative_url }}">
    <div class="project-card__media project-card__media--single">
      <img src="{{ "/assets/numalg/chirp-sketch.svg" | relative_url }}" alt="Sketch of a gravitational-wave chirp waveform" loading="lazy">
    </div>
    <div class="project-card__body">
      <h3>The sound of spacetime</h3>
      <p>How to birdwatch for a cosmic ballet.</p>
      <div class="project-card__tags">
        <span class="tag">Numerical relativity</span>
        <span class="tag">PDEs</span>
      </div>
    </div>
  </a>

  <a class="project-card" href="{{ "/numalg/willmore-flow/" | relative_url }}">
    <div class="project-card__media project-card__media--single">
      <img src="{{ "/assets/numalg/willmore-sketch.svg" | relative_url }}" alt="Sketch of a triangulated surface mesh relaxing under Willmore flow" loading="lazy">
    </div>
    <div class="project-card__body">
      <h3>A realistic conjecture?</h3>
      <p>The two-faced nature of eukariotic cell membranes.</p>
      <div class="project-card__tags">
        <span class="tag">Geometric PDEs</span>
        <span class="tag">Surface FEM</span>
      </div>
    </div>
  </a>

</div>
