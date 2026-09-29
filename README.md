# clase-7
# Sistema de turnos con Cola, Repository y pruebas unitarias

Proyecto de la **Semana 7: Patrones de Diseño, Testing Unitario y Tipos de Datos Abstractos Lineales**.

## Problema
Una oficina de atención al público necesita entregar turnos y atender a los
clientes **en orden de llegada** (primero en entrar, primero en salir). Esto se
resuelve con una **cola (FIFO)**.

## Estructura del proyecto
```
src/
  cola.py         Cola implementada a mano con nodos enlazados (sin list/deque)
  turno.py        Entidad Turno (numero, cliente)
  repositorio.py  Patrón Repository (interfaz + implementación con la Cola)
  servicio.py     Lógica de negocio; solo depende de la interfaz del repositorio
  main.py         Aplicación de consola
tests/
  test_cola.py, test_repositorio.py, test_servicio.py
```

## Operaciones de la cola
| Operación | Método | Complejidad |
|---|---|---|
| Agregar | `agregar(dato)` | O(1) |
| Eliminar | `eliminar()` | O(1) |
| Consultar siguiente | `consultar_siguiente()` | O(1) |
| ¿Está vacía? | `esta_vacia()` | O(1) |
| Cantidad | `cantidad()` | O(1) |

## Patrón Repository
`ServicioTurnos` no sabe cómo se guardan los turnos: usa la interfaz abstracta
`RepositorioTurnos`. `RepositorioTurnosCola` implementa esa interfaz sobre la
`Cola` propia. Se podría cambiar el almacenamiento (por ejemplo, una base de
datos) sin modificar la lógica de negocio.

## Requisitos
Python 3.9 o superior.

## Ejecutar la aplicación
```bash
python -m src.main
```

## Ejecutar las pruebas
```bash
pip install pytest
python -m pytest -v
```

## Ejemplo de uso en código
```python
from src.repositorio import RepositorioTurnosCola
from src.servicio import ServicioTurnos

servicio = ServicioTurnos(RepositorioTurnosCola())
servicio.solicitar_turno("Ana")     # Turno #1
servicio.solicitar_turno("Luis")    # Turno #2
servicio.ver_siguiente()            # Turno(numero=1, cliente='Ana')
servicio.atender_siguiente()        # atiende a Ana
servicio.turnos_pendientes()        # 1
```

## Pruebas incluidas
16 pruebas con **pytest** que cubren: orden FIFO, consulta sin eliminar,
errores con la cola vacía, reutilización tras vaciarla, el repositorio y las
reglas de negocio del servicio.

## Autor
Moris Espinoza 
