# adding-shadows
adding shadows to improved visual quality of your Forge-Viewer scenes





<img src="docs/shadows.mov.gif">


Set Viewer to latest dev:
```
https://autodeskviewer.com/viewers-dev/latest/viewer3D.js
```


Set a nice environment:

```
viewer=NOP_VIEWER;
viewer.setLightPreset(1);
```


Turn on Hard Shadows:

```
viewer.impl.toggleShadows(true);
viewer.impl.setShadowLightDirection(new THREE.Vector3(-1,2,1))
```



#### 4. Turn on Ambient Shadows:

``` 
viewer.impl.renderer().setAOOptions( 10, 0.1 );
```

> ie. setAOOptions(radius, darkness)


#### 5. Set to a subtle Perspective:
```
viewer.navigation.toPerspective();
viewer.setFOV(25);
```

#### Bonus:  mouse-move shadows

```
function moveShadow(x,y){ viewer.impl.setShadowLightDirection(new THREE.Vector3(x-300,y-400,600)) }

addEventListener("mousemove",function(e){moveShadow(e.clientX,e.clientY)})
```

-----


## Examples (for Fusion360)

change scale:

```
viewer.impl.renderer().setAOOptions(300, 0.7);
```

<table>
<td><img src="https://user-images.githubusercontent.com/440241/51944378-bc402180-23d0-11e9-9ee3-5a21c1a8647c.png"></td>
<td><img src="https://user-images.githubusercontent.com/440241/51944363-afbbc900-23d0-11e9-99a8-c4cca685e2f9.png"></td>
</table>

Example animation: [Steelcase Chair Assembly](https://myhub.autodesk360.com/ue29c3308/g/shares/SH7f1edQT22b515c761e167f79f6b3132118?viewState=NoIgbgDAdAjCA0IDeAdEAXAngBwKZoC40ARXAZwEsBzAOzXjQEMyzd1C0AzAJl2%2B4DGANiEBaTgBYArAE5REgOyzRAIym4BogcIUwJahQGZGhtAF8QAXSA)



## Examples (for Fusion360)

line style:

