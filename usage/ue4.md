# Usage with UE4
How to get the atmosphere woking in UE4.

There are 2 versions, a post process version and a material version.
The material version is easier to use (automatically moves when the mesh moves, light direction changes when the mesh is rotated)

### getting the assets into UE4
- download this resporitory and unzip it, find the zip file for your version, and extract it to where ue4 stores it's projects
you can find this by opening the epic games launcher and right clicking any existing project, and press 'show in folder'
- to transfer the files to a project, you'll first have to open the project you downloaded. 
- **make sure the you convert the project to the correct version (if you want to use it in a 4.23.x project, convert the project to that engine version first**. I'll add newer versions in the future)
- find the files you want to transfer (Atmosphere_mesh for the material version, atmosphere for the post process version
- select the file(s) and right click on them
- go to asset actions->migrate
- when migrating, find the content folder of the project you want to export the assets to
- select this folder and migrate the files, they should now work

### adding the atmosphere to your scene - material version
- drag the atmosphere mesh into the scene
- scale it until the atmopshere becomes fully visible
- it uses the atmosphere_instance material instance, you can edit the parameters there
- if you want multiple atmospheres with different settings, duplicate atmosphere_instance (right click it, duplicate)
- drag a new atmosphere_mesh into the scene, scale it, and set it's material to the newly created material instance
- you can now edit the new material instance to change the looks of the atmosphere

### adding the atmosphere to your scene - post process version
- put a post process volume in your scene (if you don't already have one) and set it to unbound (so the atmosphere is visible everywhere)
- recommended: create a new material instance, and set the atmosphere post process material as the parent
- under the post proces volume-> post process materials, add a new asset reference and select the atmosphere post process material (or the material instance if you made one)
- you can now edit the setting of the material instance to change the looks of the atmosphere
- multiple atmospheres is harder to do with this version, you'll first have to duplicate the atmopshere post process material (and then optionally create a new instance)
- then add the new post process material/material instance to the post process volume

### changing light direction
With the material version, you can rotate the StaticMeshInstance to change the light direction.
with the post process version, you have to change the light_direction parameter

### editing parameters
you can freely edit the parameters of the Material, here's what they do

| Parameter      | Description                                                                                                     
|:---------------|:---------------------------------------------------------------------------------------------------------------- 
| planet_radius  | how big the planet is, affects how big the atmosphere is too                                                    
| atmo_radius 	 | how big the outer sphere is, if set too low, it can cut off the atmosphere, giving an ugly effect
| beta_ray       | rayleigh scattering paramater, determines the overall color of the atmosphere
| beta_mie       | mie scattering parameter, determines the color (and intensity) of the blob around the sun
| beta_e         | scale of the parameters (10^scale) before usage, all parameters are multpiplied with 10^beta_e. changing this can improve the look in many cases
| g              | mie direction, how big the mie blob around the sun is
| height_ray     | the height scale for rayleigh, how high the rayleigh scattering goes
| height_mie     | height scale for mie, how high the mie scattering goes
| steps_i        | primary ray steps, affects quality the most, 32 is a good default (more is better, but slower)
| steps_l        | light ray steps, affects the sunset quality, 4 is the lowest before the quality becomes visibly worse (more is better, but slower)
| intensity      | the light intensity, makes the atmosphere brighet
| light_direction| the direction of the light (post process only, as it's not needed with the material version)
| planet_position| where the atmosphere is, in world space (post process only)
