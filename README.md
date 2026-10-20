# Muscle map model

`muscles.glb` is adapted from **Z-Anatomy — The libre 3D atlas of anatomy**,
by Gauthier Kervyn, based on **BodyParts3D — The Database Center for Life Science**
(Kousaku Okubo). Z-Anatomy also credits Marcin Zielinski for the Blender add-on;
no downloaded code or definitions are included in this app.

- Official source: <https://github.com/Z-Anatomy/Models-of-human-anatomy>
- Download: <https://raw.githubusercontent.com/Z-Anatomy/Models-of-human-anatomy/0189e82e4dc5c6a4ebc1d2558b78580665e9b0ef/Z-Anatomy.zip>
- Official licence and required model credits: <https://github.com/Z-Anatomy/Models-of-human-anatomy#license>
- Z-Anatomy: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
- Original BodyParts3D: [CC BY-SA 2.1 Japan](https://creativecommons.org/licenses/by-sa/2.1/jp/).
- BodyParts3D source: <https://dbarchive.biosciencedbc.jp/en/bodyparts3d/desc.html>.

Both licences permit commercial use. The derived `muscles.glb` (including the
head, hand and foot context shapes) is distributed under **CC BY-SA 4.0**. Preserve these
credits, the licence link, and this modification notice when redistributing it.
No additional restrictions are imposed on the model. The atlas lists some
non-commercial third-party organs; none of those organs are used here.

Source archive SHA-256: `e029688545627bd0214b269e1063143abb580aad72b2c2445d6d8a9a0d9da736`.

## Changes

Selected only explicitly named limb and trunk muscle meshes. Joined the left and
right sides into 37 nodes matching Gymmetry's existing muscle ids; grouped
multiple muscles where the exercise data uses a group. Split latissimus dorsi at
an approximate horizontal boundary into `upper_lats` and `lower_lats`. This is a
visual subdivision, not a claim of anatomical separation or isolation. Decimated
to roughly 900 triangles per region, removed textures and original materials,
and normalised scale. The non-selectable head, neck, hands and feet
(`body_context`) are the atlas's surface-region patches for those areas, joined,
smoothed into a plain mannequin surface and decimated. No shadows, textures,
organs, source scripts or atlas text are included.

Deep meshes retain their real positions. The screen's all-muscle list and the
sheet's deeper-muscle list make them selectable even when occluded. The hip
flexor group uses iliacus and psoas major; the adductor group uses adductor longus,
brevis, magnus, minimus and gracilis. The map groups are representative, not a
complete inventory of all muscles contributing to an action.

## Licence

`muscles.glb` is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
You may copy, adapt and redistribute it, including commercially, if you keep the credits above
and share adaptations under the same licence.

Published so the model used in the Gymmetry app's muscle map stays freely available.
