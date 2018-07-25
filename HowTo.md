Launch Camera:

roslaunch realsense2_camera rs_rgbd.launch

(Je nach launch-File werden unterschiedlich Topics veröffentlicht. Die launch-Files können jedoch so angepasst werden, dass alle benötigten Topics veröffentlicht werden)

Starte ObjectFinder.py:

navigiere zu ~/workspace/src/object_detection_rs/scripts und gebe

./ObjectFinder.py

ein.

Folgender Bildoutput ist zu erwarten:
Abstand Unterseite (die Seite auf der die Sensoren sind, und nicht der Schriftzug) der Kamera zu Boden: 67,5 cm
Abstand Unterseite  der Kamera zur Päckenoberfläche: 57,5 cm



Konsolenoutput: 

Bereich in dem Konturen erkannt werden, kann durch die Datei settings.json angegeben werden.

Für die oben gezeigten Outputs, wurden folgende Einstellungen verwendet:
  "debugging": true,
  "objects": "../objects/objects.json",
  "camera_max": 1,
  "camera_min": 0.6,
  "camera_thresh": 0.9,
  "maximal_contour_difference": 0.4,
  "minimal_contour_length": 10

debugging
True -Bildoutput; False – kein Bildoutput
objects
Pfad, an dem Objekte gespeichert werden
camera_max
Konturen, die weiter entfernt sind als camera_max werden nicht berücksichtigt [Angabe in m]
camera_min
Konturen, die näher liegen als camera_min werden nicht berücksichtigt [Angabe in m]
camera_thresh

maximal_contour_difference
Legt fest wie groß der Unterschied zwischen zwei Konturen maximal sein darf, damit das Objekt getrackt wird
minimal_contour_length
Minimale Länge einer Kontur. Konturen werden als Vektor von Punkten gespeichert. Dieser Parameter bestimmt somit die minimale Länge des Vektors


Kamera spezifische Details werden in der settingsCamera.json angegeben:

Für den oben gezeigten Output wurden folgende Einstellungen verwendet:

  "unit":1000,
  "DepthImageTopic":"/camera/depth/image_rect_raw",
  "PointCloudTopic":"/camera/depth/color/points"

unit
Die Tiefenkameras veröffentlichen ihre Tiefeninformation in verschiedenen Einheiten.
Unit = 1 →  Kamera veröffentlicht in [m]
Unit = 1000 → Kamera veröffentlicht in [mm]
DepthImageTopic
Vollständiger Name des Ros-Topics über das, das Tiefenbild veröffentlicht wird
PointCloudTopic
Vollständiger Name des Ros-Topics über das die PointCloud veröffentlicht wird


Veröffentlichte Topics


object_recognition/position_midpoint:
mit Workaround
	Vektor (x = Anzahl der px in x Richtung, 0 ist links;
		 y = Anzahl der px in y Richtung 0 ist oben;
		 z = 0 )

ohne Workaround
	Vektor( x = Verschiebung in x Richtung in [m];
		 y = Verschiebung in y Richtung in [m];
		 z = Abstand zum Objekt in [m])
		
object_recognition/orientation: 
	Vektor: normalisierter Richtungsvektor (z = 0)
