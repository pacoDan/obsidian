Perfecto. Tienes dos videos `.mp4` y sus respectivos audios separados `.m4a`. Puedes unir cada pareja con FFmpeg para obtener dos videos finales con audio y video sincronizados, sin recodificar y conservando la calidad original.

Abre PowerShell en `C:\Users\Daniel\Downloads\videos_redes` y ejecuta estos comandos.

## 1. Unir HDLC + Frame Relay

```ps1
ffmpeg -i "HDLC+Frame Relay (2021-06-04).mp4" -i "HDLC+Frame Relay (2021-06-04).m4a" -map 0:v:0 -map 1:a:0 -c copy -shortest "HDLC+Frame Relay (2021-06-04) FINAL.mp4"
```

## 2. Unir TCP Redes de Información

```ps1
ffmpeg -i "TCP Redes de Información K4573 (2021-10-22 at 1506 GMT-7).mp4" -i "TCP Redes de Información K4573 (2021-10-22 at 1506 GMT-7).m4a" -map 0:v:0 -map 1:a:0 -c copy -shortest "TCP Redes de Información K4573 FINAL.mp4"
```

## ¿Qué hace cada opción?

- `-i`: indica los archivos de entrada.  
    
- `-map 0:v:0`: utiliza el video del primer archivo.  
    
- `-map 1:a:0`: utiliza el audio del segundo archivo.  
    
- `-c copy`: copia ambos flujos sin recodificar, por lo que el proceso es rápido y no pierde calidad.  
    
- `-shortest`: termina el archivo cuando finaliza el flujo más corto.  
    
- `.mp4`: contenedor del video final.  
    

## Resultado esperado

En la misma carpeta tendrás estos dos archivos nuevos:

- `HDLC+Frame Relay (2021-06-04) FINAL.mp4`  
    
- `TCP Redes de Información K4573 FINAL.mp4`  
    

Los archivos originales permanecerán intactos.

Importante: `-shortest` puede recortar el final si el audio y el video tienen duraciones distintas. Si quieres conservar toda la duración del video original, puedes quitar esa opción. Además, estos comandos presuponen que ambos archivos de cada pareja comienzan en el mismo instante; si el audio tiene un desfase inicial, habrá que ajustar la sincronización.

Si PowerShell indica que `ffmpeg` no se reconoce como comando, necesitarás instalar FFmpeg o agregarlo al `PATH` de Windows.