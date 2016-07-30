# Atmospheric Scattering for Unity 5
[![IMAGE ALT TEXT HERE](https://0rvyea-dm2305.files.1drv.com/y3mUj3cTFGBT8_5qaqKL83ApLubUWp-oLOWq56s7KCDuGuQb9LO9vP6F88XjKPlBt8JIV_vQmMlkT9lMzn8vOoXwTMuVyL8bpoIx3ajVu-jCR8rmLMSzFcnraINNH1mm7URUxsRzqECpkjK0YStARBudQ?width=1403&height=639&cropmode=none)](https://youtu.be/MC6MKYHllX0)

Open source (FreeBSD) atmospheric scattering for Unity 5. Features precomputed physically based atmospheric scattering (single scattering at the moment). It can render skybox, atmospheric fog, light shafts and global reflection probe (only skybox is reflected). It can also control directional and ambient light color/intensity. All parts can be turned on and off at any time.

**_Important:_** This is a hobby project without any official support. I don't intent to use it in any real world application. Use it at your own risk.

Corresponding Unity forum thread can be found [here]().

See the demo scenes on Youtube [here](https://youtu.be/yCKhQFHybLc) and [here](https://youtu.be/MC6MKYHllX0)

##### Sister project
[Volumetric Lights for Unity](https://github.com/SlightlyMad/VolumetricLights)

### Roadmap
TBD
(I plan to continue working on it but no promises)

### Requirements
* Unity 5 (tested on 5.3.4)
* Requires Compute shaders -> requires DirectX 11 or equivalent 
* Tested on Windows/DX11 only but it should work on other platforms as well
* Tested only with deferred rendering path

### Usage
* Add AtmosphericScattering script to your camera.
* Set your main directional light as a sun. (AtmosphericScattering script/General Settings/Sun)
* Set AtmosphericScattering compute shader (AtmosphericScattering script/General Settings/Compute Shader) 
* Create material with "Skybox/AtmosphericScattering" shader and set it as skybox in Window/Lighting/Skybox.
* Set Camera clear flags to "Skybox"

See included sample scenes for examples.

#### Building a standalone player
**_IMPORTANT_** - Standalone player will work only if all shaders are included in build! All shaders must be added into "Always Included Shaders" in ProjectSettings/Graphics.

#### Atmospheric Scattering Parameters
##### General Settings
* Compute Shader - atmospheric scattering compute shader. Must be set.
* Sun - directional light that will represent the sun. Must be set.

##### Atmospheric Scattering
* Render Atm Fog - toggle atmospheric fog rendering
* Incoming light - Amount of light that enters atmosphere.
* Rayleigh Coef - Rayleigh scattering coefficient
* Mie Coef - Mie scattering coefficient
* MieG - Parameter used by mie phase function. Controls amount of light scattered based on light's direction
* Distance Scale - Atmospheric fog is computed for Earth like planet. It takes several kilometers before you can see any fog. Use this parameter to tweak the fog for the size of your scene 

##### Sun disk
* Render Sun - toggle sun disk rendering
* Sun Intensity - controls sun disk size/intensity

##### Directional Light
* Update Color - update dir light color/intensity every frame
* Intensity - dir light intensity multiplier

##### Ambient Light
* Update Color - update ambient light color/intensity every frame
* Intensity - ambient light intensity multiplier

##### Light Shafts
* Enable Light Shafts - toggle light shafts (note that dir light shadows must be turned on for the light shafts to work)
* Quality - light shafts rendering resolution/quality
* Sample Count - number of ray-marching samples (more samples -> better quality -> worse performance)

##### Reflection Probe
* Enable reflection probe - creates/enables global reflection probe. It is updated in real-time. Only skybox is reflected.
* Resolution - reflection probe resolution

### Known Limitations
* It is a physically based technique. It gives you limited options to tweak the visual result. That may change slightly in the future

### Technique overview
##### Skybox rendering
Atmospheric Scattering is precomputed for every altitude, camera angle nad light angle. Based on [Elek09]. Sun/camera azimuth is omitted for better performance (3D lookup table is sufficient). See [Bruneton08] if you want higher quality (requires 4D lookup table).

##### Atmospheric fog
Numerically integrated every frame at very low resolution and stored in 3D lookup table for future use.

##### Directional/Ambient light color
Precomputed for every time of day [Bruneton08]. Stored in 1D look up tables. 

##### Light Shafts
Light shafts are not physically based. Computed separately and used to multiply atmospheric scattering during post-processing. Based on ray-marching. Retrofitted from [Volumetric Lights project](https://github.com/SlightlyMad/VolumetricLights).

### Possible improvements
* Quality and performance can be improved
* Shaders aren't very well optimized
* Multiple scattering for more realistic atmosphere
* More customization options

### Donations
I've been asked about donation button several times now. I don't feel very comfortable about it. I don't need the money. I have a well paid job. It could also give the impression that I would use the money for further development. But that is certainly not the case. 

But if you really like it and you want to brighten my day then you can always buy me a little gift. Send me [Amazon](https://www.amazon.com/Amazon-Amazon-com-eGift-Cards/dp/BT00DC6QU4) or [Steam](https://www.paypal-gifts.com/uk/brands/steam-digital-wallet-code.html) gift card and I'll buy myself something shiny. You can find my email in my profile. 

### References
* [Elek09] [Rendering Parametrizable Planetary Atmospheres with Multiple Scattering in Real-Time](http://www.cescg.org/CESCG-2009/papers/PragueCUNI-Elek-Oskar09.pdf)
* [Bruneton08] [Precomputed Atmospheric Scattering](https://hal.inria.fr/inria-00288758/document)
* [Yusov13] [Outdoor Light Scattering](https://software.intel.com/en-us/articles/outdoor-light-scattering-sample-update)

[![IMAGE ALT TEXT HERE](https://bauhvg-dm2305.files.1drv.com/y3m8OSwfrspmuoi3zAr89mg3oNUx21i_WQXOj0Mh8YaUCw0UYFIuWUVTQfT4LZ1dKDZ0BQF67ViApoG6U5ipB8xmXhx5nu9XmzpvAVrRYSWNg3NjU2Q6OVV3bZwC60XHgdqCrxR6o2JvWmIwya_Vdm7Q3r-Eha3HoIM18DnlWtQ1aU?width=1920&height=2160&cropmode=none)](https://youtu.be/yCKhQFHybLc)