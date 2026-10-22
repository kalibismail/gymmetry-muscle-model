# Muscle map model

`muscles.glb` and `muscles-detail.glb` are adapted from **Z-Anatomy — The libre 3D atlas of anatomy**,
by Gauthier Kervyn, based on **BodyParts3D — The Database Center for Life Science**
(Kousaku Okubo). Z-Anatomy also credits Marcin Zielinski for the Blender add-on;
no downloaded code or definitions are included in this app.

- Official source: <https://github.com/Z-Anatomy/Models-of-human-anatomy>
- Download: <https://raw.githubusercontent.com/Z-Anatomy/Models-of-human-anatomy/0189e82e4dc5c6a4ebc1d2558b78580665e9b0ef/Z-Anatomy.zip>
- Official licence and required model credits: <https://github.com/Z-Anatomy/Models-of-human-anatomy#license>
- Z-Anatomy: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
- Original BodyParts3D: [CC BY-SA 2.1 Japan](https://creativecommons.org/licenses/by-sa/2.1/jp/).
- BodyParts3D source: <https://dbarchive.biosciencedbc.jp/en/bodyparts3d/desc.html>.

Both licences permit commercial use. The derived `muscles.glb` and
`muscles-detail.glb` (including the head, bone and tendon context shapes) are
distributed under **CC BY-SA 4.0**. Preserve these
credits, the licence link, and this modification notice when redistributing it.
No additional restrictions are imposed on the model. The atlas lists some
non-commercial third-party organs; none of those organs are used here.

Source archive SHA-256: `e029688545627bd0214b269e1063143abb580aad72b2c2445d6d8a9a0d9da736`.

## Changes

Selected only explicitly named muscle meshes. Joined the left and right sides
into 44 region nodes: 37 matching Gymmetry's existing muscle ids, plus seven
map-only regions (front of neck, back of neck, hand muscles, foot muscles, deep
hip rotators, fibularis muscles, breathing muscles); grouped multiple muscles
where the exercise data uses a group. Within a region, each atlas muscle (or a
small set of atlas parts shown as one, such as the three columns of iliocostalis)
is kept as its own primitive, named after the app's child muscle id, so the app
can highlight and pick a single muscle once its region is selected. There are
136 such child primitives across 27 regions; the other 17 regions are a single
muscle. Muscles that are entirely internal (pectoralis minor, subclavius,
rotatores, multifidus, the deep hip rotators, gluteus minimus, popliteus,
supinator, pronator quadratus, the intercostals, diaphragm, pyramidalis and the
small deep neck and hyoid muscles, 31 in all) live in `muscles-detail.glb` as
`<region>.detail` nodes, which the app downloads the first time a region with
children is selected and merges into that region. Parted latissimus dorsi into
`upper_lats` and `lower_lats` after decimation and shading, on a line rising
towards the armpit, both halves sharing the seam's vertices, normals and
shading and neither capped. This is a visual subdivision, not a claim of anatomical
separation or isolation. The thin aponeurotic parts of the lats, gluteus
maximus, obliques, lower trapezius and serratus anterior are smoothed again
after decimation so their edges stay clean. The
atlas's "ascending" and "descending" trapezius parts are mapped to the upper and
lower trapezius respectively, matching where they sit on the body rather than
their atlas names. Softened the surface fibre texture, decimated to roughly 900
triangles per region (up to 2,600 for the flat abdominal and chest sheets, the
forearm tendons, the breathing muscles and the small hand and foot muscles),
sharing each region's budget between its muscles in proportion to surface area
with a floor of 160 triangles per muscle, removed textures and original
materials, and normalised scale. The obliques and transversus abdominis
have their front aponeuroses trimmed medial to the rectus abdominis, so the
rectus is the surface muscle over the front of the abdomen.

Five non-selectable context nodes hold the head and the parts that show between
the bare muscles, one per tissue so each can have its own material.
`body_context` is the head: the atlas's surface-region patches for the face,
ears and scalp (no neck patches), joined from the left half and mirrored, capped
flat at the jaw and skull base, subdivided once, smoothed into a plain mannequin
surface and decimated. Decimated hard, `context_bone` carries the bones of the
hands and feet, the tibia and fibula, the clavicles, hyoid, thyroid and cricoid
cartilages and trachea, and the manubrium, which is moved back into the chest,
scaled down and shaded darker so the sternal notch sits quietly between the
collarbones; `context_tendon` the calcaneal tendon and the
tendon of extensor digitorum longus. The deep leg muscles (extensor digitorum and
hallucis longus, fibularis longus, brevis and tertius, tibialis posterior, flexor
digitorum and hallucis longus) are selectable children of the tibialis anterior,
fibularis and soleus regions. `context_skin` is a
see-through shell over each hand and foot from the atlas's skin patches, cut
open at the wrist and just above the ankle, subdivided, smoothed and decimated,
with a vertex alpha that fades to clear at the open edges.

Every solid node carries a baked vertex colour: ambient occlusion sampled with
hemisphere rays against the whole body, and on the muscles a paler tint where
the mesh is thin, which is where a muscle has become tendon or aponeurosis. No
shadows, textures, organs, source scripts or atlas text are included.

Deep meshes retain their real positions. The screen's all-muscle list and the
sheet's deeper-muscle list make them selectable even when occluded. The hip
flexor group uses iliacus and psoas major; the adductor group uses adductor longus,
brevis, magnus, minimus and gracilis. The front-of-neck group is the
sternocleidomastoid, scalenes, infrahyoids, digastric, mylohyoid, longus colli
and longus capitis; the back-of-neck group is splenius capitis and colli,
semispinalis colli, spinalis and longissimus capitis and levator scapulae. The
hand group is the thenar and hypothenar muscles, interossei and lumbricals; the
foot group is the short extensors, abductors, flexors, adductor hallucis,
quadratus plantae, lumbricals and interossei. The deep hip rotator group is
piriformis, obturator internus and externus, the gemelli and quadratus femoris;
the breathing group is the diaphragm, intercostals, subcostales, transversus
thoracis, serratus posterior and levatores costarum. The map groups are
representative, not a complete inventory of all muscles contributing to an action.

## Rebuild

Download to a new empty directory outside the repository. Extract **only**
`Z-Anatomy/Startup.blend`; do not install the template or run its Python scripts.
Use Blender's factory settings and disable automatic execution:

```sh
/snap/bin/blender --background --factory-startup --disable-autoexec \
  --python scripts/build-muscle-model.py -- \
  /absolute/path/to/Startup.blend assets/models/muscles.glb \
  assets/models/muscles-detail.glb
```

The script appends only the explicitly listed mesh objects, not the source scene,
drivers or scripts. No Draco/meshopt decoder is needed: the uncompressed main model is
already below the 3 MB budget and the detail file is about 0.25 MB, and works with the same loader on native and web.
