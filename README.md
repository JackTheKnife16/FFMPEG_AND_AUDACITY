# FFMPEG AND AUDACITY
Cosas para editar videos simples usando FFMPEG para manipular videos y Audacity para mejorar audios

## FFMPEG
En esta parte haremos cosas basicas pero de mucha utilidad, como cortar videos en un rango de tiempo determinado, unir videos, unir video con audio, etc...

### Cortar Videos
Este es el comando para cortar videos en un rango determinado de tiempo:

```{r, engine='bash', count_lines}
ffmpeg -ss 00:01:47.50 -i input.mp4 -t 00:02:02.50 output.mp4
```
### Unir un Audio a un Video
Con el siguiente comando se puede unir un archivo de audio con uno de video

```{r, engine='bash', count_lines}
ffmpeg -i video.mp4 -i audio.mp3 -map 0:v -map 1:a -c:v copy -c:a copy output.mp4 -y
```

### Unir varios Videos
En caso de que sean videos con diferentes formatos o resoluciones:

```{r, engine='bash', count_lines}
ffmpeg -i opening.mkv -i episode.mkv -i ending.mkv \
-filter_complex "[0:v] [0:a] [1:v] [1:a] [2:v] [2:a] \
concat=n=3:v=1:a=1 [v] [a]" \
-map "[v]" -map "[a]" output.mkv
```
En el caso de que no haya problema con el formato o resolucion:
1. primero se debe crear una lista de los archivos que se quieren unir en un solo archivo.
```{r, engine='bash', count_lines}
echo file <filename1>.mp4 > lista.txt
echo file <filename2>.mp4 >> lista.txt
.......
echo file <filenameN>.mp4 >> lista.txt
```
2. correr el siguiente comando:
```{r, engine='bash', count_lines}
ffmpeg -f concat -safe 0 -i lista.txt -c copy output.mp4
```

## AUDACITY
Esto es lo que debemos hacer si queremos mejorar el audio aumentando su volumen:
https://www.youtube.com/watch?v=s30sOdfuX90

En el siguiente video se puede ver como quitar el sonido de fondo:
https://www.youtube.com/watch?v=7Me8BrCA7PY&t=231s
