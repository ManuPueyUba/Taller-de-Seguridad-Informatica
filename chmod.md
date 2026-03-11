# chmod

## Qué es chmod?

chmod significa change mode y se usa para cambiar los permisos de archivos o directorios en Linux.

Los permisos controlan quién puede:

- r → read (leer)
- w → write (escribir)
- x → execute (ejecutar)

Estos permisos se aplican a tres grupos de usuarios:

``` bash
usuario (u) | grupo (g) | otros (o)
```

## Cómo funciona el modelo de permisos en Linux

Ejemplo:

Se ignora el primer guion (-)
```bash
-rwxr-xr--
```

Se separa así:
```bash
rwx | r-x | r--
```
Osea el usuario puede hacer todo 
- read
- write 
- execute

El Grupo solo puede 
- read
- cant write
- execute

El gion actua como un 0 o una ausencia de permiso

Los permisos siempre son en ese orden R -> W -> X

Cada permiso tiene un valor
Read -> 4
Write -> 2
Execute -> 1

## Tabla de valores numéricos
Entonces se pueden sumar para poner un valor directo

| Valor | Permisos | Suma |
|-------|----------|------|
| 7 | rwx | 4 + 2 + 1 |
| 6 | rw- | 4 + 2 |
| 5 | r-x | 4 + 1 |
| 4 | r-- | 4 |
| 3 | -wx | 2 + 1 |
| 2 | -w- | 2 |
| 1 | --x | 1 |


## Ver permisos actuales

``` bash
ls -l archivo
```

Si un archivo tiene 
```bash
rw-
```
Se puede abrir y editar, pero no ejecutar

Ejemplo:

``` bash
rw-r--r-- 1 kali kali 1679 Mar 10 clave.pem
```

Esto se interpreta asi:

``` bash
rw- r-- r--
│   │   │
│   │   └── otros
│   └────── grupo
└────────── dueño
```

## Formas de usar chmod

Forma simbólica (más intuitiva)

```bash
chmod <Who><+ -><r w x>
```

Basicamente es:
chmod quien tipo permiso

quien -> u g o
tipo -> + || - 
permiso -> r w x

### Agregar permiso:
```bash
chmod u+x archivo
```

```bash
u → usuario (dueño)
+ → agregar permiso
x → ejecutar
```
Resultado:

👉 el dueño ahora puede ejecutar el archivo.

### Caso Real
Tenemos un script

```bash
backup.sh
```
Pero al ejecutar el script con:

```bash
./backup.sh
```
sale:

```bash
Permission denied
```

Entonces hacés:

```bash
chmod u+x backup.sh
```

### Eliminar permisos

```bash
chmod g-w archivo
```
significa
```bash
g → grupo
- → quitar permiso
w → escritura
```
Resultado:

👉 el grupo ya no puede modificar el archivo.

### Caso Real
En un servidor:
```bash
config.conf
```
Solo el administrador debería modificarlo.

Entonces le sacás permiso de escritura al grupo para evitar cambios accidentales.
