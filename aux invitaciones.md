Perfecto. Entonces el script debe detectar automáticamente todos los videos de invitaciones, independientemente de su nombre (`tio-marcos.mp4`, `prima-laura.mp4`, `amigo-juan.mp4`, etc.), usando siempre los mismos archivos `final.mp4` y `audio.mp3`.

Este script procesa todos los `.mp4` de la carpeta, excepto `final.mp4` y los videos ya generados que terminan en `completo.mp4`.

## Script `procesar.sh`

bash

```sh

#!/bin/bash

set -e

VIDEO_FINAL="final.mp4"
AUDIO="audio.mp3"

# Comprobar que existen los archivos comunes
if [[ ! -f "$VIDEO_FINAL" || ! -f "$AUDIO" ]]; then
    echo "Error: falta final.mp4 o audio.mp3"
    exit 1
fi

# Buscar todos los MP4 de la carpeta
for video in *.mp4; do

    # Si no hay archivos coincidentes, salir del bucle
    [[ -f "$video" ]] || continue

    # Excluir el video final y los resultados anteriores
    [[ "$video" == "$VIDEO_FINAL" ]] && continue
    [[ "$video" == *completo.mp4 ]] && continue

    # Crear el nombre de salida
    nombre="${video%.mp4}"
    salida="${nombre}completo.mp4"

    echo "Procesando: $video -> $salida"

    ffmpeg -y \
        -i "$video" \
        -i "$VIDEO_FINAL" \
        -i "$AUDIO" \
        -filter_complex \
        "[0:v]setpts=PTS-STARTPTS[v0]; \
         [1:v]setpts=PTS-STARTPTS[v1]; \
         [v0][v1]concat=n=2:v=1:a=0[v]" \
        -map "[v]" \
        -map 2:a:0 \
        -c:v libx264 \
        -preset veryfast \
        -crf 23 \
        -c:a aac \
        -b:a 192k \
        -shortest \
        "$salida"

done

echo "¡Todas las invitaciones han sido procesadas!"
```

## Ejemplo de los archivos

Entrada:

text

```
audio.mp3
final.mp4
tio-marcos.mp4
prima-laura.mp4
amigo-juan.mp4
abuela-maria.mp4
```

Salida:

text

```
tio-marcoscompleto.mp4
prima-lauracompleto.mp4
amigo-juancompleto.mp4
abuela-mariacompleto.mp4
```

## Cómo ejecutarlo

bash

```
chmod +x procesar.sh
./procesar.sh
```

Importante: este script vuelve a codificar el video para poder concatenarlo, lo que permite combinar videos con distintas características en muchos casos, aunque deben ser compatibles en resolución y parámetros de formato para evitar errores.

Además, `-shortest` corta el resultado cuando termina la pista más corta entre el video concatenado y `audio.mp3`. Si necesitas que el audio se escuche completo, habría que ajustar esa opción según la duración de tu audio.