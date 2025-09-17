# lab02-debugging

Muqiao Lei

[Shader - Shadertoy BETA](https://www.shadertoy.com/view/tflfWf)

## Bugs Found and Fixed

### Bug 1: Incorrect Aspect Ratio Calculation

**Location**:  line 8 **Original Code**:

H *= len * iResolution.x / iResolution.x;

**Fixed Code**:

H *= len * iResolution.x / iResolution.y;

**How I found it**: Noticed `iResolution.x / iResolution.x` always equals 1, which provides no aspect ratio correction.

### Bug 2: Invalid Variable Type Declaration

**Location**:  line 68 **Original Code**:

vec uv2 = 2.0 * uv - vec2(1.0);

**Fixed Code**:

vec2 uv2 = 2.0 * uv - vec2(1.0);

**How I found it**: Shader compilation failed because `vec` is not a valid GLSL type.

### Bug 3: Incorrect reflect() Function Parameters

**Location**:   line 48 **Original Code**:

dir = reflect(eye, nor);

**Fixed Code**:

dir = reflect(dir, nor);

**How I found it**: The `reflect()` function requires (incident_direction, normal), not (eye_position, normal).

### Bug 4: Wrong UV Coordinates Passed to Raycast

**Location**:  line 71 **Original Code**:

raycast(uv, dir, eye, ref);

**Fixed Code**:

raycast(uv2, dir, eye, ref);

**How I found it**: Code calculated `uv2` but used wrong `uv` coordinates for camera projection.

### Bug 5: Insufficient Raymarching Iterations

**Location**:  line 13 **Original Code**:

for(int i = 0; i < 64; ++i) {

**Fixed Code**:

for(int i = 0; i < 128; ++i) {

**How I found it**: 64 iterations weren't sufficient to reach distant floor geometry from camera position.

# Setup

Create a [Shadertoy account](https://www.shadertoy.com/). Either fork this shadertoy, or create a new shadertoy and copy the code from the [Debugging Puzzle](https://www.shadertoy.com/view/flGfRc).

Let's practice debugging! We have a broken shader. It should produce output that looks like this:
[Unbelievably beautiful shader](https://user-images.githubusercontent.com/1758825/200729570-8e10a37a-345d-4aff-8eff-6baf54a32a40.webm)

It don't do that. Correct THREE of the FIVE bugs that are messing up the output. You are STRONGLY ENCOURAGED to work with a partner and pair program to force you to talk about your debugging thought process out loud.

Extra credit if you can find all FIVE bugs.

# Submission

- Create a pull request to this repository
- In the README, include the names of both your team members
- In the README, create a link to your shader toy solution with the bugs corrected
- In the README, describe each bug you found and include a sentence about HOW you found it.
- Make sure all three of your shadertoys are set to UNLISTED or PUBLIC (so we can see them!)
