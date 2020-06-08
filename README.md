# ForgeViewer - Shadows and Lighting

UPDATE: material background: http://help.autodesk.com/view/ARENDERING/ENU/?guid=GUID-97CC0DD3-35A8-4D8F-80A0-B1C4AD54D2B0

How to add shadows to Forge-Viewer

<img src="docs/shadows.mov.gif">


### Steps

##### 1. Set Viewer to latest dev:
```
https://autodeskviewer.com/viewers-dev/latest/viewer3D.js
```


##### 2. Set a nice environment:

```
viewer=NOP_VIEWER;
viewer.setLightPreset(1);
```

##### 3. Turn on Hard Shadows:

```
viewer.impl.toggleShadows(true);
viewer.impl.setShadowLightDirection(new THREE.Vector3(-1,2,1))
```



##### 4. Turn on Ambient Shadows:

``` 
viewer.impl.renderer().setAOOptions( 10, 0.1 );
```

> ie. setAOOptions(radius, darkness)


##### 5. Set to a subtle Perspective:
```
viewer.navigation.toPerspective();
viewer.setFOV(25);
```

##### Bonus:  mouse-move shadows

```
function moveShadow(x,y){ viewer.impl.setShadowLightDirection(new THREE.Vector3(x-300,y-400,600)) }

addEventListener("mousemove",function(e){moveShadow(e.clientX,e.clientY)})
```

-


# Fusion360 content Examples


#### [Jeldwen Doors / Windows](https://youtu.be/lNlG00ZVUyI?t=4523) - Adding AO and hard shadows...

![](https://user-images.githubusercontent.com/440241/52377772-dc588c00-2a33-11e9-9a35-5e2d8539a361.png)


#### [Steelcase Chair Assembly](https://myhub.autodesk360.com/ue29c3308/g/shares/SH7f1edQT22b515c761e167f79f6b3132118?viewState=NoIgbgDAdAjCA0IDeAdEAXAngBwKZoC40ARXAZwEsBzAOzXjQEMyzd1C0AzAJl2%2B4DGANiEBaTgBYArAE5REgOyzRAIym4BogcIUwJahQGZGhtAF8QAXSA) - with sunset/studio Environment lighting

Another one: [Table Assembly Animation](http://assemblyinstructionviewer.steelcase.com/Viewer/AssemblyDirectionViewer?AssemblyDirectionID=13588)

Jeldwen website: http://assemblyinstructionviewer.steelcase.com/Viewer/AssemblyDirectionViewer?AssemblyDirectionID=3171

<table>
<td><img src="https://user-images.githubusercontent.com/440241/51944378-bc402180-23d0-11e9-9ee3-5a21c1a8647c.png"></td>
<td><img src="https://user-images.githubusercontent.com/440241/51944363-afbbc900-23d0-11e9-99a8-c4cca685e2f9.png"></td>
</table>


### Set AO scale, for Fusion files:

```
viewer.impl.renderer().setAOOptions(300, 0.7);
```


# BONUS Section

### Sharper SAO (Scalable Ambient Obscurancy)

1. pull the latest version of viewer3D.js (https://developer.api.autodesk.com/modelderivative/v2/viewers/6.5.2/viewer3D.js)
2. search/replace `define SCALE` and change scale value from `(2)` to `(1)` 

This will have a small rendering performance hit on "pixel fill rate" (so, zoom-in full screen and GPU slow down might happen when 'smooth navigation' flag is off).

To use the modified viewer, just use "Chrome-ReDirector" from the chrome webstore.


### Sharper IBL Reflections (Image Based Light, ie. skybox)
Forge Viewer environment maps (.DDS files) are only 128px x 128px resolution ... TINY!  So reflections looks blurry and metal looks dusty.
So, to improve reflections, we need to make them sharper.  

To do that, we need to create our own .DDS files, using this v. CMD tool: https://github.com/wallabyway/cubemapgen
It quickly converts your custom .HDR or .EXR skybox file into a .DDS file for Forge Viewer.

Here's sharper reflections with a custom "RiverBank.EXR" environment map at 256px x 256px.

Looking better already !!!
![sharper-SAO+IBL](https://user-images.githubusercontent.com/440241/54461156-071bbb80-4729-11e9-86b6-30b249b7f631.jpg)

Also, with sharper SAO.


### Changing line style:

```
viewer.impl.setPostProcessParameter("style", "edging");
viewer.impl.setPostProcessParameter("brightness",1.0);

```
![](https://user-images.githubusercontent.com/440241/51944553-340e4c00-23d1-11e9-9c5e-7c4eb9e34674.png)




## Improving Materials

This is the general workflow, in Fusion...

![](https://user-images.githubusercontent.com/440241/51944564-396b9680-23d1-11e9-9e5b-c94067b5b6f0.png)

#### 1. Use Fusion 'Render mode' to pick better materials 
![](https://user-images.githubusercontent.com/440241/51944571-3f617780-23d1-11e9-80dd-7e8dd0f1f54f.png)

#### 2. How to add custom materials / Decals

- Adding a custom texture, like cardboard : [YOUTUBE](https://www.youtube.com/watch?v=D9AS5rQhtPo)
- adding decals:  [YOUTUBE](https://www.youtube.com/watch?v=ASLb5BesBrg)
