# Time Lapse amb software de codi obert sobre Windows i també aplicable a Linux.


Normalment treballo amb Linux, però sé que la majoria de vatros treballeu amb Windows, per això he intentat trobar eines de codi obert que pogueu fer servir en aquest sistema (i que a més a més funcionin amb Linux).

Un Time Lapse és un vídeo fet a partir d'una seqüència de imatges fetes a intervals regulars, i permet mostrar el moviment accelerat de canvis que succeeixen a poc a poc. Podem veure un exemple bonic en aquesta pàgina: https://www.pond5.com/es/stock-footage/453957/time-lapse-apertura-y-morir-dahlia-rojo-9b-con-alfa-mate.html


### Fer les fotos

En aquest taller només explicaré com processar les fotos, per fer les fotos us caldrà una càmera que tingui la funció de fer fotos a intervals regulars. Podeu fer servir un mòbil  amb l'ajut d'alguna aplicació que us permeti aquesta funcionalitat, cerqueu a Internet els termes "intervalometer app" i segur que en trobareu alguna que us serveixi.

A l'hora de fer les fotos hi ha alguns consells que cal tenir en compte. En primer lloc per evitar diferències entre les fotos cal fer servir els mateixos ajustaments, això vol dir que hem de fer les fotos en mode manual i fixar paràmetres que la majoria de càmares ajusten de forma automàtica, com poden ser autoenfocament, balanç automàtic de blancs, ajustament automàtic de ISO, compensació de la exposició....

Les diferències entre fotos provoquen un efecte en el video que s'anomena "flickering" i que molesta una mica. Hi ha algunes eines que poden ajudar a reduïr-lo. No he trobat cap eina lliure per Windows, per Linux he fet servir aquesta eina: https://github.com/cyberang3l/timelapse-deflicker

Cal agafar una àrea més àmpla de la que necessitem, ja ho ajustarem amb més cura després.

El video en FullHD té una resolució de 1920x1080, inferior a 3 MPixels. La majoria de fotos caldrà escalar-les (reduïr la mida). Una resolució de 5MPX és més que suficient, si feu servir resolucions molt més altes les fotos us ocuparàn molt d'espai i no conseguireu una gran millora en la qualitat. Evidentment, si voleu ver videos 4K haureu de fer fotos amb més resolució.

El format RAW ocupa molt més però resulta més adient per fer post-processament, ja que evitem els artefactes produïts per la compressió en formats com jpg el "problema" que té aquest format és que els arxius amb les imatges ocupen molt més lloc.

Cal decidir l'interval de temps entre fotografies, en funció del resultat esperat. Hi ha eines que poden ajudar-nos a fer càlculs, com per exemple https://www.omnicalculator.com/other/time-lapse Cal tenir en compte que per una bona percepció del moviment hem de fer servir al menys unes 10-12 imatges per cada segon de vídeo. Depenent del ràpid que canvii l'escena caldrà definir l'interval entre fotos.

Potser us caldrà eliminar o retocar algunes fotos degut a que apareixen per un moment elements inesperats que distorsionarien el vídeo. Podeu generar el vídeo i si al mirar-lo noteu algun efecte "estrany" intenteu localitzar els fotogrames afectats i corregir-los. Un programa de retoc d'imatges com Photoshop (comercial) o Gimp (lliure) us servirà per aquesta tasca.



### Fer el Time-Lapse


un cop teniu les fotos, fer un vídeo a partir de una seqüencia d'imatges implica les següents fases:

- Processar les fotos. Principalment cal seleccionar l'àrea de la foto a incloure en el vídeo, i intentar millorar la qualitat de les imatges. Ho farem amb el programa DarkTable que podeu descarregar de: https://www.darktable.org/install/
  - Retallar per ajustar a la mida del vídeo que es vol.
  - Corregir color i exposició
  - Qualsevol altra millora o efecte que volguem aplicar

- Opcionalment es pot fer el que s'anomena "deflicker" que consisteix en intentar emparellar les condicions de iluminació de les fotos. Si no es fa la imatge mostra una mena de "tremolor" degut a les diferències de iluminació entre les fotos fetes en diferents moments.

- Generar el vídeo a partir de la seqüència de imatges, afegir una pista de Audio i renderitzar el vídeo en format MP4. Ho farem amb el programa Blender que podeu descarregar de: https://www.blender.org/download/


Per aquest taller utilitzaré una colecció de fotos del procés de floridura d'un prèssic, "apropiades" del treball de recerca de la meva filla.


### Passos a fer amb DarkTable per processar les fotos

- Importar la carpeta amb les imatges originals a processar.

- Editar la primera imatge a la cambra fosca (fent doble click o anant al menú de la part superior dreta)

- Retallar la imatge amb la proporció segons la pantalla (16:9, 4:3...). Cal fer servir les eines del grup bàsic, la que diu "escapça i gira".

- Fer qualsevol altra millora o aplicar filtres per afegir efectes.

- Un cop la imatge al vostre gust, torneu a la taula de llum i a la opció de la dreta on fica "pila de l'historial" escolliu copia-ho tot. Això ens copiarà tots els canvis fets a la imatge.

- Seleccioneu totes les altres imatges i feu clic a "enganxa tot" a la mateixa pila de l'historial. S'aplicaran tots els canvis a la resta de imatges.

- A la dreta, baix de tot despleguem "opcions d'emmagatzematge" i exportem les imatges en format "JPEG (8-bit)". Revisem la carpeta de destí i fem clic a exporta.



### Passos a fer amb Blender per generar el vídeo

Blender no és un programa d'edició de vídeo, és principalment conegut per les seves capacitas d'animació 3D. Podeu veure un exemple del que es podia fer fa 10 anys amb aquest programa en aquest curt: https://www.youtube.com/watch?v=YE7VzlLtp-4

Per generar el Time Lapse a partir de les fotos fetes hem de seguir aquestos passos:

- Definir la mida del vídeo a la part dreta on posa "Dimensions". Hi ha diferents presets, escollim el més adient segons la qualitat dessitjada i el format a que hem retallat les fotos (16:9, 4:3...)

- Definir el format de sortida del vídeo a la part inferior dreta de la pantalla principal, on posa "output". 
  - Escollir la carpeta on es desarà la sortida
  - Triar "FFmpeg video" com a format de sortida
  - Triar el preset "h264 in MP4" en "Encoding"

- Al menú superior canviar la vista "Default" per "Video Editing"

- A la part inferior, en l'editor de seqüències, fer click al botó "Add" i després "Image" anar a la carpeta on es troben les imatges, fer clic a la primera, anar a la darrera i fer Ctrl+Shift+Click per tal de seleccionar-les totes. Això les carrega en el que anomena un "Stripe" i mostra el nombre d'imatges carregades.
  - Canviar "End" a la part inferior pel nombre de imatges carregades, de forma que el vídeo les mostri totes.

- Afegir una pista d'audio. Al mateix lloc fer "Add" i "Sound". Es pot moure la pista d'audio

- A la part inferior, a "Playback" marcar les opcions "Audio Scrubbing", "AV sync" i "frame dropping" Això permetrà veure el vídeo i sentir l'àudio en sincronia.

- Podem desar totes les configuracions fetes de forma que apareguin al engegar el programa. Cal anar a "File" al menú superior i "Save Startup File".

- Per seleccionar un "Stripe" al editor de seqüència cal fer servir el botó dret del ratolí!!

- Cal assegurar-se que la resolució del vídeo i de les imatges coincideix, ja que si no ho fa les imatges seran convertides i es pot perdre detall.

- La tecla "Inici" del teclat mostra tots els stripes al editor.

- Si volem afegir un altre vídeo cal tenir en compte la resolució i el framerate. Blender permet canviar la resolució, però si el framerate no coincideix caldrà fer servir un altra eina per transcodificar-lo. Una molt bona opció per transcodificar vídeo és HandBrake.

- Amb blender podem afegir imatges, text, efectes... Es un editor molt complert, però potser no el més senzill de fer servir. La dificultat de aprendre el seu funcionament es compensa amb la flexibilitat que ofereix un cop hi estas familiaritzat

- Un cop ja tenim a punt el nostre projecte cal anar a les propietats, i dalt de tot, a "Render" fer click a "Animation". Es generarà un vídeo a la carpeta seleccionada a "Output". Si volem veure com es va generant el vídeo, a "Display" podem seleccionar "New Window" i ho veurem en una finestra sobre el Blender.



### Software que podeu fer servir

- Eina per processar les fotos, es troba tant per Windows com per Linux.
  - https://www.darktable.org/

- Eina per fer el vídeo, es troba tant per Windows com per Linux. Permet fer moltes altres coses!!!
  - https://www.blender.org/

- Editor de audio per retallar i millorar les pistes de àudio.
  - https://www.audacityteam.org/

- Eina per treure flickering per a Windows (pagament)
  - https://timelapsedeflicker.com/

- Eina per treure flickering per a Linux (lliure)
  - https://github.com/cyberang3l/timelapse-deflicker

- Eina per transcodificar vídeos en diferents formats.
  - https://handbrake.fr/


### Crèdits

Principals pàgines de Internet que he fet servir (no hi són totes)

- Tutorial de com fer un TimeLapse. Veureu que explica pràcticament el mateix que hem fet en aquest taller.
  - http://joegiampaoli.blogspot.com/2015/04/creating-time-lapse-videos-mostly-in.html

- 27 vídeos de cóm fer servir Blender. Estàn en anglès, però s'entenen molt bé, estàn molt ben explicats i es mostra pas a pas el procés. Totalment recomanables si penseu fer servir aquesta eina.
  - https://www.youtube.com/playlist?list=PLjyuVPBuorqIhlqZtoIvnAVQ3x18sNev4

- Tutorial de com fer servir Blender
  - https://sites.google.com/site/alistargazing/home/image-processing/processing-toolbox/blender-tutorial


