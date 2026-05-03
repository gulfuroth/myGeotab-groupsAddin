# Fleet Org — MyGeotab Add-in

**Fleet Org** es un add-in para MyGeotab que permite visualizar y gestionar la jerarquía de grupos de flota directamente desde la plataforma.

## Características

- **Visualización jerárquica** — treemap interactivo y vista árbol (mindmap) de grupos
- **Tabla de dispositivos** — búsqueda avanzada con filtros por nombre, plan, serie, odómetro…
- **Sintaxis de lista** — `[V1 V2 V3]` como OR rápido para buscar varios valores
- **Modo edición** — añadir/eliminar dispositivos de grupos, crear grupos, borrar grupos vacíos
- **Cambios encolados** — todos los cambios se revisan en un modal de confirmación antes de aplicarlos
- **Indicador de progreso** — para operaciones grandes (> 10 cambios)
- **Idiomas** — inglés, español, alemán

## Instalación en MyGeotab

1. En MyGeotab ve a **Administración → Sistema → Add-ins**
2. Haz clic en **Nuevo** y pega la siguiente URL del manifest:

```
https://raw.githubusercontent.com/gulfuroth/myGeotab-groupsAddin/refs/heads/main/addin-manifest.json
```

3. Guarda y recarga. El add-in aparecerá en el menú de Administración como **Groups Management**.

## Estructura del repositorio

```
addin/
  index.html      — interfaz principal (minificada)
  app.js          — lógica de la aplicación (minificada)
  styles.css      — estilos (minificados)
  icon.svg        — icono del add-in
addin-manifest.json — manifest para MyGeotab
```

> Este repositorio contiene únicamente el **build de distribución**. El código fuente se encuentra en [gulfuroth/fleetorg-addin](https://github.com/gulfuroth/fleetorg-addin).

## Versiones

| Versión | Descripción |
|---------|-------------|
| v1.3.0  | Búsqueda con listas `[...]`, cambios encolados coherentes, progreso en operaciones grandes, borrado de grupos vacíos |
| v1.2.0  | Traducción alemán, barra Quick Links, UX odómetro, redimensión de columnas, filtro de búsqueda de grupos |
| v1.0.0  | Versión inicial: gestión de grupos, treemap, modo edición, tabla de dispositivos |
