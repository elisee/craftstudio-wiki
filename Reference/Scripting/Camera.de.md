# Camera component API

----
## Camera:SetProjectionMode, Camera:GetProjectionMode

```lua
Camera:SetProjectionMode( --[[ Projizierungs Modus (ProjectionMode) ]])

-- Gibt "ProjectionMode" zurück
Camera:GetProjectionMode()
```

Setzt oder gibt den Modus der Kameraprojektion wieder. Mögliche Werte sind:
 ```Camera.ProjectionMode.Perspective``` und```Camera.ProjectionMode.Orthographic```.

### Beispiel: **Ändere den Modus der Kameraprojektion**

```lua
local cameraRndr = CS.FindGameObject( "Ein Objekt mit einem Kamera Renderer" ).camera
cameraRndr:SetProjectionMode( Camera.ProjectionMode.Orthographic )
```
----
## Camera:SetFOV, Camera:GetFOV
```lua
?Camera:SetFOV( --[[ FOV (number) ]] )

-- Gibt die FOV der Kamera als Nummer aus
?Camera:GetFOV()
```

Setzt oder gibt den Wert des vertikalen Sichtfeldes der Kamera in Grad aus.
Valide Werte sind 1° bis 179°

Wird nur genutzt wenn der Modus der Kameraprojektion auf ```perspective``` steht.

----
## Camera:SetOrthographicScale, Camera:GetOrthographicScale
```lua
?Camera:SetOrthographicScale( --[[ scale (number)]] )
-- Gibt den Wert der Skalierung wieder
Camera:GetOrthographicScale()
```

Setzt oder gibt die orthographische Skalierung der Kamera wieder. Je größer die Skalierung, je größer das Sichtfeld der Kamera.

Wird nur genutzt wenn der Modus der Kameraprojektion auf ```orthographic``` steht.

----
## Camera:SetRenderViewportPosition / Camera:SetRenderViewportSize, Camera:GetRenderViewportPosition / Camera:GetRenderViewportSize
```lua
Camera:SetRenderViewportPosition( --[[ position x (nummer) ]], --[[ position y (nummer) ]] )
Camera:SetRenderViewportSize( --[[ breite (nummer) ]], --[[ höhe (nummer) ]] )

-- Gibt eine Tabelle mit der Ansichtsfenster (ViewPoint) Position wieder
Camera:GetRenderViewportPosition()

-- Gibt eine Tabelle mit der Größe des Ansichtsfensters (ViewPoint) wieder
 Camera:GetRenderViewportSize()
```
Setzt oder gibt die Position und Größe des Ansichtsfensters des Kamerarenderers wieder. Dies kann dazu genutzt werden um Split-Screen Multiplayer zu realisieren. 

Die Werte sind normalisiert, dass heißt, sie sollten im Bereich von 0.0 (links / oben) bis 1.0 (unten / rechts) liegen.

Beispielweise könntest du zwei Kamera mit der Größe (1.0, 0.5) haben. Eine Oben bei (0,0) und die andere Unten bei (0, 0.5).

Die wiedergegebenen Tabellen für die getters enthalten zwei Nummern, gespeichert als ```.x``` und ```.y``` Eigenschaften.

----
## Camera:CreateRay
```lua
-- Gibt einen Strahl wieder.
Camera:CreateRay( --[[ Eine Tabelle mit den Bildschirmkoordinaten x,y (tabelle) ]] )
```
Erzeugt einen Strahl der an den angegebenen Koordinaten (x, y) der Kamera startet und forwärts geht.

Dies kann für "mouse picking" und andere ähnliche Aktionen genutzt werden. Schau dieses [raycast demo video](http://www.youtube.com/watch?v=V1nz1xnEDKY) (Englisch) als Beispiel.

----
## Camera:Project
```lua
-- Gibt eine Tabelle wieder
Camera:Project( --[[ position (Vector3) ]] )
```

Projiziert eine 3D Raum Position zu einer 2D Bildschirm Position.
Die wiedergegebene Tabelle enthält die Koordinaten des projizierten Bildschirm als ```.x``` und ```.y``` Eigenschaften.

Diese Funktion könnte dazu genutzt werden um die 2D Bildschirmposition eines Charakters oder Objektes mit der Hauptkamera zu bekommenund einen Strahl zu erzeugen um 2D Interface Elemente auf der sekundären orthographischen Kamera zu rendern.