# WTP_TarpTool
## Summary
Tool allows generation of cloth-like meshes via physical simulation, from input mesh actor(s) used as tarp(cloth) input and one or multiple actors used as colliding static geometry to simulate input cloth against, using gravity as the main driving force of the simulation. Output mesh, when baked to an actor, is automatically nanite enabled with UVs, normals and material assignments.
## Quick Start Guide
* Instanciate the tool by dragging the `WTP_TarpTool_X_X` HoudiniAsset from the content browser into the level.

![Screenshot_4](https://github.com/user-attachments/assets/d6cf96e6-61d5-4b09-8430-366a0234a7b1)

* Spawned tool needs two inputs provided, both are actors in the level.

![Screenshot_1](https://github.com/user-attachments/assets/a9eac81f-3551-42a6-81fe-b370bee72f94)

* First provide an actor mesh or multiple meshes that will be used as the tarp(cloth) meshes by clicking the **Start Selection** button in the **Input Shape** section of the **Inputs** tab.

![Screenshot_2](https://github.com/user-attachments/assets/3addd0ad-c73f-4096-9624-bcc74b6d2fb8)

* After finishing selecting actors in the level click the **Use Current** button. You will notice the **Currently Selected Actors** section got populated with actors you have defined.

![Screenshot_5](https://github.com/user-attachments/assets/8491fa39-a3b4-4836-ba1a-b865e10674ff)
![Screenshot_6](https://github.com/user-attachments/assets/4998f06f-fe63-4f38-9032-9ff67cbc01c4)

* Secondly we need to provide collider actors. Click **Start Selection** in the **Colliders** section of the **Inputs** tab. After you are done with you actor selection, click **Use Current** to commit the selection.

![Screenshot_7](https://github.com/user-attachments/assets/92abcaf3-8f53-414a-a57c-5590e1b527ee)
![Screenshot_8](https://github.com/user-attachments/assets/b95c9c9a-d356-4eb4-b10e-9d23c91717d4)

* Hide actors that were used as input for the tarp(cloth) shape, so they are not obstructing the view.
* Switch to the **Parameters** tab and tick the **Enable Simulation** checkbox to activate simulation calculations. This will force Houdini to cook and calculate, allow it to finish, that can be identified by both your tarp(cloth) updated state in the level and a notification from Houdini Engine in the lower right corner stating **Finished Proccessing Output**.

![Screenshot_9](https://github.com/user-attachments/assets/5f9a5959-befa-4788-b7b0-06812915e98a)
![Screenshot_10](https://github.com/user-attachments/assets/7e6d5846-4a90-4f3b-8486-c4a3dabf4c0a)

* When changing position of the input meshes or changing any of the parameters in the **Parameters** tab of the interface, press the **Rerun Simulation** button to re-simulate the tarp(cloth).

![Screenshot_11](https://github.com/user-attachments/assets/c470a427-fbe9-4984-84d6-fc6dcbbe6d9a)

## Tool Parameters
### Inputs Tab
![Screenshot_12](https://github.com/user-attachments/assets/af5fd95e-3e53-4725-9b95-c9085cac547b)
Parameter | Description
----------------- | ---
`World Input Shape` | Level selection parameter, define actors that will be used as tarp(cloth) shape(s).
`World Input Colliders` | Level selection parameter, define actors that will be used as static colliders for the simulation. 

### Parameters Tab
![Screenshot_13](https://github.com/user-attachments/assets/58f85def-5219-46b5-a0ae-8c69dcca78a1)
Parameter | Description
--- | ---
`Enable Simulation` | Global checkbox to enable/disable simulation calculations, if disabled still outputs input shape remeshed, UVe with material assignments, with any changes to the shape.
`Rerun Simulation` | Radius away from pole, in meters, that is used when placing guy-wire hooks for the current pole.
`Sim Mesh Resolution` | Triangle side size of the remeshed input geometry. Resolution of the simulation.
### Parameters Tab | Sim Settings
Parameter | Description
--- | ---
`Use Ground Plane` | Toggle virtual indefinate ground plane as a collider, a cheaper version of providing a ground/landscape actor.
`Ground Height Position` | World Z position of the virtual ground plane.
`Material Density` | Density of the physical material used in calculations of the simulation, how dense is the cloth of the tarp.
`Material Stretch Resist` | Resistance of the physical material to stretching.
`Material Bend Resist` | Resistance of the physical material to bending.
`Colliders Friction` | Friction multiplier for collider geometry, resists cloth sliding along it. Default value of 10 makes colliders very sticky.
### Parameters Tab | Mesh Post-Processing
Parameter | Description
--- | ---
`Spatial Blur` | Spatial blur of the output mesh point positions, helps to relax sharp details.
`Subdivide Depth` | Post-simulation output geometry subdivision, helps add detail to the output geometry.
`Detangle Result` | Toggle the detangle algorithm. Algorithm tries to solve and fix self-intersections and collider intersections.
`Remesh Output` | Select type of final remeshing logic.
. | `No Remeshing` - output geometry as is, no final remeshing.
. | `Uniform` - uniform triangle remeshing based on the **Remesh Uniform Size** parameter size.
. | `Adaptive` - adaptive remeshing, areas that require more resotion will get higher triangle density, based on **Remesh Min/Max Size** parameters.
### Parameters Tab | Material
Parameter | Description
--- | ---
`UV Scaling` | Scaling multiplier of the mesh UVs. Allows for mesh-side control over texture repetition and other UV related effects.
`Material Instance` | Select material instance to be assigned to the output mesh.

### Defaults Tab
![Screenshot_14](https://github.com/user-attachments/assets/7639ef1f-e7d3-41a2-8e8f-d1819e1c0c1f)
Parameter | Description
----------------- | ---
`Frames To Simulate` | Number of frames to simulate, could be raised if the results of the simulation look unresolved, still floating or overall not converged to desired state.
