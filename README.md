# tlcl-labs

Labs prácticos para *The Linux Command Line* (William Shotts). Cada lab levanta un
escenario en un contenedor Docker con algo para resolver, y un `check` valida si lo
lograste. La idea es practicar en la terminal lo que se lee en cada capítulo, no
memorizar comandos.

## Requisitos

- Docker
- Bash

## Uso rápido

```bash
./lab list              # lista todos los labs disponibles
./lab start 10-1        # levanta el lab 1 del capítulo 10 y abre una shell adentro
check                   # (dentro del lab) valida tu solución
exit                    # sale del lab
./lab reset 10-1        # vuelve el lab a su estado inicial
```

## Comandos

| Comando                  | Qué hace                                              |
|--------------------------|-------------------------------------------------------|
| `./lab list`             | Lista los labs con su estado (pendiente / resuelto)   |
| `./lab start <cap>-<n>`  | Construye el escenario y abre una shell en el lab     |
| `./lab reset <cap>-<n>`  | Destruye el contenedor y recrea el escenario          |
| `./lab verify <cap>-<n>` | Corre la verificación automática del lab (ver abajo)  |
| `check`                  | Dentro del contenedor: valida la solución             |

## Estructura

```
.
├── Dockerfile              # imagen base (Ubuntu)
├── lab                     # CLI para manejar los labs
└── labs/
    └── 10-procesos/
        └── 10-1/
            ├── README.md   # consigna (sin la solución)
            ├── setup.sh    # arma el escenario
            ├── check.sh    # valida y da feedback
            └── solution.sh # solución de referencia
```

## Cómo hacer un lab

1. Leé el capítulo correspondiente del libro.
2. Levantá el lab y leé la consigna con `cat README.md` dentro del contenedor.
3. Resolvelo usando solo la terminal. Si te trabás, usá `man`, `--help` o volvé al libro.
4. Corré `check`. Si falla, el mensaje te dice qué falta, no cómo hacerlo.
5. Recién cuando pase, mirá `solution.sh` y compará enfoques.

No mires `solution.sh` antes de resolverlo. Es la regla que hace que esto sirva.

## Verificación de labs

Cada lab debe cumplir:

- `check.sh` **falla** sobre el escenario recién creado.
- `check.sh` **pasa** después de correr `solution.sh`.

`./lab verify <cap>-<n>` hace las dos pruebas. `./lab verify all` las corre sobre
todos los labs. Un lab que no pasa la verificación se considera roto.

## Cobertura

| Parte                          | Capítulos | Estado      |
|--------------------------------|-----------|-------------|
| 1. Learning the Shell          | 1–10      | En progreso |
| 2. Configuration & Environment | 11–13     | Pendiente   |
| 3. Common Tasks & Tools        | 14–23     | Pendiente   |
| 4. Writing Shell Scripts       | 24–36     | Pendiente   |

Capítulos que se saltean o adaptan:

- **vi:** salteado (uso Neovim a diario).
- **Impresión:** salteado.
- **Almacenamiento y redes:** requieren permisos especiales en Docker; se adaptan
  o se practican directamente en el VPS.

## Agregar labs nuevos

1. Crear la carpeta `labs/<cap>-<tema>/<cap>-<n>/` con los cuatro archivos.
2. La consigna describe un problema realista (algo roto, info a extraer, una tarea
   concreta), no "ejecutá el comando X".
3. `check.sh` da feedback útil sin revelar la solución.
4. Correr `./lab verify <cap>-<n>` antes de commitear.
