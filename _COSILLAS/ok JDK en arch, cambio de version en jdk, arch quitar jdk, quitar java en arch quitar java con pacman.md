
en lugar de quitar podemos setear otro por defecto:

- Ver qué versiones de Java tienes instaladas:
    
    ```sh
    archlinux-java status
    ```
    
- Cambiar la versión por defecto a la que prefieras (reemplaza `java-17-openjdk` o el nombre que liste el comando anterior por la tuya):
```sh
sudo archlinux-java set <nombre-de-la-version>
```

en mi caso fue:
```sh
sudo archlinux-java set java-17-amazon-corretto
```