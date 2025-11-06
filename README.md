# [Untitled]

"If you want to bake an apple pie from scratch, you must first invent the universe"

### Building a chick ragdoll agent

This is in a general a difficult problem. But let us treat this as best as we can. The aim is to create a realistic chick agent so that we have a biomechanically approximate model to run developmental experiments on. 3D biomechanical models, even those that are obtained through dissection are always approximate: https://nmbl.stanford.edu/publications/pdf/Hutchinson2015.pdf. We can be optimistic because we have several resources available to us. The resources include existing avian musculoskeletal models, particularly the OstrichRL model, frameworks for the fast, mature biomechanical simulation that is open source (MuJoCo), and several studies on avian anatomy and allometry, which provides measurements that will be useful. 

A most simple thought, starting with the OstrichRL model, would be to scale it down to "chick" size, and call it a model. This would take us suprisingly close. In fact, I estimate this would take us about 90% there already. But it does not fully work. In fact, it is quite impossible to go past the 90% barrier. The rest of this section is dedicated to the remainder of the 10%, of which, we hope to capture 5% at the limit, minimum. 


#### Background & Bones:

To build a musculoskeletal biomechanical body, we require two things: skeleton, and musculature. By skeleton, I refer not only to an accurate-as-possible digital representation of the bones, but also to their physical properties and overall arrangement. By musculature, I refer not only to the origin and insertion points (points where the muscle attaches to the bone) but also their wiring and mechanistic properties such as force. OR, we could just use the laws of allometry, which can be inferred (list of references)

The best bet for accurate-as-possible digital bones, would be to extract them from a CT scan. However, scanned bones (.stl file) usually have some faces missing or have self intersecting, “see-through” geometry. Basically, they are not very good meshes. There is usually a mesh processing or mesh cleaning process, such as https://roboti.us/lab/papers/XuBioRob12.pdf where new faces are fitted to the scan geometry. Our approach will be to voxelize and then remesh it. This is an accurate, and much simpler process, one which does not need depend on access to state-of-the-art (read expensive) bone scanning and reconstruction software. 

Coming back to briefly to the issue of obtaining the bone meshes, it is not possible to do so. There exist no publically available CT scans of a chicken (gallus gallus) in the public domain, let alone that of a chick. There also do not exist any scanned freely available meshes of a chicken skeleton. Further, allometric scaling does not work. Cosider the following: (ostrich example) .

BUT, there exists a real scan of an assembled skeleton from a show at a musesum, which can be used as reference to model the meshes of the said bones in a 3D software like Blender or Maya. I would say that's where we can start. 

List of sources:
* Muesum scan of assembled chicken skeleton
* Papers related to measurements

#### Muscles

The far more important thing about biomechanical simulation, though, is its musculoskeletal aspect. By which I specifically refer to the points of attachments of the tendons to the bone, and the range of force that can be applied by the muscle. The propagation of the force, of course, is offleaded to be taken care of by the simulation software, MuJoCo.  

One issue is that it is quite difficult to accurately determine the muscle origin and insertion sites without access to the organism. All the models that exist, OstrichRL, Beagel, are made by referencing measurements off a dissection, an option we do not have at the moment. The good news is that we're trying to model aves, and we have a model for ostrich (also beloning to aves, of course) that we can reference our model after. We can do so, using non-rigid 3D shape registration, and allometric scaling. 



List of sources:
* Muesum scan of assembled chicken skeleton
* Papers related to measurements



#### Useful Excerpts
https://roboti.us/lab/papers/XuBioRob12.pdf

“In order to accurately match the size and shape of the
human finger bones. We used the index finger from a Stratasys
Corporation’s laser-scan model of human left hand bones
supplied in STL format, imported the tessellate facets into
Pro/Engineer, and created solid models for each bone by fitting
new surfaces to the scan geometry.”
