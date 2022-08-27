# Car-Parking-Simulator-V1
Our groupproject about the first implementation of the game "Car-Parking Simulator".

# Lern-Bericht
Car-Parking Simulator V1 - Julian Hartmann (https://github.com/JHartmann-ims), Benjamin Peterhans

## Einleitung

Uns wurde die Aufgabe gegeben, in einer Gruppe oder in Einzelarbeit ein Projekt zu erstellen. Als Gruppe, also Julian Hartmann und ich, haben uns die Aufgabe gegeben, ein 3d Spiel für handybasierte Systeme zu erstellen. Wir sollten mit den Softwares Blender und Unity klarkommen und dieses Projekt mithilfe dieser Programme gestalten.

## Ziele

Meine Ziele:

Z1: Ich kann mit Unity Editor arbeiten

Z2: Ich komme mit der Programmiersprache C# klar

Z3: Ich kann einige Methoden, bzw. Funktionen von Unity anwenden

Z4: Ich kann ein Spiel designen und funktionsfähig implementieren

## Beschreibung

Wir, also Julian Hartmann und ich, haben uns vorgenommen, ein Spiel zu entwickeln. Das Spiel ist ein «Car-Parking»-Simulator, wobei es darum geht, ein Auto in einen Parkplatz zu steuern. Dabei gibt es einige Hindernisse, und zwar andere Autos, die auf dem Parkplatz herumstehen. Insgesamt gibt es hierfür drei individuelle Levels, die man spielen kann. Da dieses Spiel handybasiert ist, gibt es für das Steuern des Autos vier Buttons: das Vorwärtsfahren, Rückwärtsfahren, Rechtslenken und das Linkslenken. Die Bremse des Autos wird automatisch betätigt, sobald das Auto nicht mehr vor- oder rückwärts fährt.
Natürlich gibt es für ein Handyspiel ein GUI, beziehungsweise ein Menü, in dem man herumnavigieren kann. Im Spiel selbst kann man das Menü betätigen und einige Funktionen auswählen, wie zum Beispiel das Neustarten des Spiels, das Auswählen der Levels, das Beenden des Spiels etc.

## Demo

[![IMAGE ALT TEXT](http://img.youtube.com/vi/Bgnr378WKJc/0.jpg)](http://www.youtube.com/watch?v=Bgnr378WKJc "Car-Parking Simulator V1")

## Codeausschnitt

```cs
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;
using UnityEngine.EventSystems;
using UnityEngine.UI;
using System.Collections.ObjectModel;

namespace carControl
{
    [System.Serializable]
    public class AxleInfo
    {
        public WheelCollider leftWheel;
        public WheelCollider rightWheel;
        public bool brake;
        public bool motor;
        public bool steering;
    }

    public class CarControl : MonoBehaviour//, IPointerDownHandler, IPointerClickHandler
    {
        [SerializeField] public List<AxleInfo> axleInfos;
        public float maxMotorTorque;
        public float maxSteeringAngle;
        public float maxBrakeForce;

        public void HandleCar(float verticalInput, float horizontalInput, bool isBraking)
        {
            float motor = maxMotorTorque * verticalInput;
            float steering = maxSteeringAngle * horizontalInput;
            float brake = isBraking ? maxBrakeForce : 0f;

            foreach(AxleInfo axleInfo in axleInfos)
            {
                if (axleInfo.steering)
                {
                    axleInfo.leftWheel.steerAngle = steering;
                    axleInfo.rightWheel.steerAngle = steering;
                }
                if (axleInfo.motor)
                {
                    axleInfo.leftWheel.motorTorque = motor;
                    axleInfo.rightWheel.motorTorque = motor;                    
                }
                axleInfo.leftWheel.brakeTorque = brake;
                axleInfo.rightWheel.brakeTorque = brake;
                ApplyLocalPositionToVisuals(axleInfo.leftWheel);
                ApplyLocalPositionToVisuals(axleInfo.rightWheel);
            }
        }
    }
}
```

# Download

Downloadlink: https://drive.google.com/drive/folders/1mdXhwB4u-J0WXi0NjWKQHL07UV97b7DF?usp=sharing

## Verifikation

Z1: Wird mit dem Projekt und den 'Scenes' (unter 'ILA_1305_Car-Parking\Assets\Scenes') validiert.

Z2: Wird mit dem Beispielcode nebenan und den CS-Dateien (unter ILA_1305_Car-Parking\Assets\Scripts) validiert.

Z3: Wird mit den Zeilen 35 bis 46 im Beispielcode nebenan validiert.

Z4: Wird mit der Produktdemonstration validiert.

# Reflektion zum Arbeitsprozess

##### IPERKA

I: Da dieses Projekt in Homeoffice erarbeitet wurde, habe ich mich entschieden, mit jemand neuem ein Projekt zu gestalten. Ich habe mich also dann mit Julian Hartmann zusammengetan, um ein Projekt für uns zu implementieren. Für die Auswahl des Projektes haben wir uns relativ viel Zeit genommen, da es viele gute Vorschläge von Themen gab. Da wir beide unsere in einen neuen Bereich der Programmierwelt wagen wollten, kamen wir zum Schluss, ein Spiel für handybasierte Systeme zu programmieren. Da jetzt viel Neues im Bereich Game-Development uns entgegenkam, mussten wir uns zuerst in Blender und Unity einarbeiten. Bei der Informationssammlung und der Einarbeitung hat mir Blender etwas Mühe bereitet, da die Funktionen dort sehr umfangreich und auch kompliziert sind. In Unity hingegen lief dies um einiges besser.

P: Wie im letzten Projekt habe ich die Arbeitspakete erstellt, wobei mir aufgefallen ist, dass dieses Projekt sehr umfangreich wird.

E: Es wurde entschieden, dass das Projekt per OneDrive geteilt wird, sodass wir beide jederzeit Zugriff darauf hatten.

R: Hauptsächlich war ich in diesem Projekt mit Unity beschäftigt gewesen. Mehrheitlich war ich für die Funktionsweisen des Spiels zuständig. Da dieses Projekt für mich neu war, gab es einige Stolpersteine, die mir Mühe, Frustrationen und Kopfschmerzen bereiteten. Jedoch gab es auch bestimmte Momente, bei denen ich mich gefreut habe, wenn ich zum Beispiel einen funktionierenden Lösungsweg gefunden habe.

Die Implementation des GUIs, beziehungsweise des Menüs, bereiteten mir keine wirklichen Probleme. Dafür musste ich lediglich ein Canvas in Unity erstellen, wo ich dann Texte und Buttons hineinziehen kann. Für das Öffnen von den verschiedenen Levels habe ich als Hilfe den "Link 2" benutzt.

Als Nächstes begab ich mich für das Einsetzten von verschiedenen Objekten, in diesem Fall Autos, die auf dem Parkplatz herumstanden. Für alle Objekte, die auf dem Parkplatz stehen, musste ich Colliders und sogenannte "Rigidbodies" hinzufügen. Colliders sind um Grunde genommen feste Objekte, die einen Festkörper haben. Ein "Rigidbody" ist ein Effekt für die Gravitation der Objekte. Auch hier hatte ich wenig Probleme bei der Implementierung.

Was mir aber sehr viel Mühe bereite, war das Steuern des Fahrzeugs. Ich habe im Internet nach Tutorials gesucht, wie man ein Auto zum Fahren bringt, was mir zum einen Teil weiterhalf, aber beim anderen Teil nicht. Mit dem Tutorial unter dem "Link 3" konnte ich ein Programm kreieren, was das Fahrzeug fortbewegte, aber jedoch nur mit den Keyboard-Tasten. Mit den Methoden "OnPointerDown" und "OnPointerUp" habe ich versucht, so die Buttons mitzuintegrieren. Das Problem jedoch war, dass sich das Auto manchmal nur nach vorne bewegen konnte, nach hinten aber nicht. Mit verschiedenen Lösungsansätzen im Kopf versuchte ich dieses Problem zu lösen, was aber vergeblich war. Es gab auch einmal einen Moment, wo das Fahrzeug rückwärts fahren konnte, aber wiederum nach vorne nicht. Die meiste Zeit habe ich damit verbracht, eine Lösung zu finden, und habe so sehr viel Zeit hineininvestiert und gleichzeitig auch verschwendet. Erst gegen Ende des Projektes habe ich den "Link 1" gefunden, der mir bei diesem Problem weiterhalf und somit das Problem gelöst hat.

K: Am Schluss lief das Programm einwandfrei, auch wenn es einige Funktionen noch nicht gab.

A: Mit dem Auswerten konnte ich über das Projekt etwas reflektieren. Wir beide haben dann am Schluss noch unsere Meinungen geteilt, was zum Beispiel eher schiefgelaufen ist, oder auch was gut ging. Das Projekt gefiel mir sehr, da ich einen neuen Einblick in eine teilweise andere Programmierwelt hatte. Ich habe sehr vieles gelernt, was mir auch sehr viel Spass machte.

## Links

Link 1: https://docs.unity3d.com/Manual/WheelColliderTutorial.html

Link 2: https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadScene.html

Link 3: https://www.youtube.com/watch?v=Z4HA8zJhGEk&t=1s
