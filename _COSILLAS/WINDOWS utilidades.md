asociar .json a notepad++ desde cmd
Desde CMD como administrador para asociar los archivos `.json` con Notepad++ ubicado en `C:\Program Files\Notepad++`.

```sh
ftype NotepadPlusPlus="C:\Program Files\Notepad++\notepad++.exe" "%1"
assoc .json=NotepadPlusPlus
```

----
----

QUITAR StartIsBack

El mensaje real que estás viendo en tu notebook es: ==**"Hold Escape key to disable StartIsBack from loading"**==. [[1](https://forospyware.com/t/startisback/23167)]

Tu sistema mezcló las palabras "Escape" con _Endscape_ y "StartIsBack" con _Startis black_. Esto es lo que significa y los pasos para quitarlo:

¿Qué es y para qué sirve?

**[StartIsBack](https://www.google.com/url?sa=i&source=web&rct=j&url=https://www.startisback.com/&ved=2ahUKEwi2hOLYnr-XAxUYIbkGHbmtO-4Qy_kOegoIAggACAAIDxAC&opi=89978449&cd&psig=AOvVaw1R18wIeJNsDbAnQ8vFqFjZ&ust=1792264232755000)** es un programa de personalización para Windows. Sirve principalmente para **cambiar el diseño del menú de inicio y la barra de tareas** (por ejemplo, para que tu Windows 10 o 11 se vea y funcione con el menú clásico de Windows 7). [[1](https://www.filehorse.com/es/download-startisback/), [2](https://www.reddit.com/r/Windows11/comments/1c4y7b1/startisback_startallback_which_one_is_the_real_one/?tl=es-419)]

El aviso que ves al arrancar es solo una advertencia del programa que te indica que, si mantienes presionada la tecla **Esc (Escape)** mientras la computadora enciende, evitarás que el programa se cargue en ese inicio. Normalmente aparece cuando el programa se instaló de forma incompleta, es una versión de prueba que ya caducó, o está teniendo un fallo de compatibilidad. [[1](https://translate.google.com/translate?u=https://apps.microsoft.com/detail/xpfmhkp3qhrqrh?hl%3Den-US%26gl%3DUS&hl=es&sl=en&tl=es&client=sge), [2](https://forospyware.com/t/startisback/23167)]

---

¿Cómo desactivarla o eliminarla por completo?

Si no utilizas este programa y quieres que el aviso deje de aparecer, lo mejor es desinstalarlo siguiendo estos pasos:

- Presiona las teclas **Windows + R** en tu teclado para abrir la ventana de "Ejecutar".

- Escribe `appwiz.cpl` y presiona **Enter** (esto abrirá la lista de programas instalados).

- Busca en la lista **StartIsBack** o **StartAllBack** (su versión más reciente).

- Haz clic derecho sobre él y selecciona **Desinstalar**.

- Reinicia tu notebook. Con esto, el cartel desaparecerá para siempre


-----
-----

Everything comandos

```sh
ext:lnk;exe word
```
