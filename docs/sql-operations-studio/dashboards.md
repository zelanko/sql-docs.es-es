---
title: "Obtener acceso rápidamente a información y tareas comunes en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo mostrar widgets de detalle en las operaciones de SQL Studio (versión preliminar)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b501b653920d2a8ff7e3e8ed4656c8154b344f6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>Paneles en[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Para ver un panel, el menú contextual de un servidor o la base de datos y seleccione **administrar**.

![Panel de ejemplo](media/dashboards/sample-dashboard.png)

**Propiedades del servidor** contiene las propiedades del servidor, incluida la versión, edición, nombre de equipo y versión del sistema operativo.

**Tareas** contiene commons tareas como la restauración y la nueva consulta.

**Buscar bases de datos** fácil buscar bases de datos existentes almacenados en el servidor, incluidas las tablas.

**Estado de copia de seguridad** buscar fácilmente el estado de copia de seguridad de bases de datos existentes.

## <a name="configuring-insight-widgets"></a>Configuración de una visión general de Widgets
Se recomienda que siga el tutorial para configurar el panel, que puede encontrarse [aquí](tutorial-build-custom-insight-sql-server.md).

Además, asegúrese de que desproteja el ["Cómo..." sobre la configuración de widgets de insight]().

Después de seguir este tutorial, siga leyendo para obtener más información sobre los widgets específicos que no se tratan en el tutorial.

## <a name="insight-detail"></a>Detalles de una perspectiva
La ventana flotante detalles de información proporciona información más detallada de un widget de información relacionados. 
- Un widget de Insight representa una vista de resumen de un vistazo con recuento, línea, gráfico etcetera. 
- La ventana flotante detalles de información proporciona detalles "explorar", enumerar un poco más información sobre los datos para cada elemento mostrado en el widget de una visión general de alto nivel. 
  - El contenido de la ventana flotante detalles se define con una consulta SQL independiente para la consulta del widget principal. 

No hay ningún requisito de conjunto para una consulta de detalles de una visión general, pero el diseño es estándar.
- La mitad superior de la vista siempre es una vista "Resumen" de la columna 2. Las columnas que desea usar se definen mediante las propiedades de "etiqueta" y "value" de la configuración de JSON
- Al hacer clic en una fila de la tabla de resumen, la parte inferior la mitad de la ventana flotante mostrará el conjunto completo de información de columna para esa fila.

### <a name="insight-detail-configuration-in-packagejson"></a>Configuración de detalle de una visión general de package.json

Configuración de ventana flotante de detalles de una visión general de ejemplo
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```
|propiedad|Tipo|value|Valor predeterminado|description|comment|
|:---|:---|:---|:---|:---|:---|
|detalles|objeto JSON|||propiedad obligatoria para definir las definiciones de detalle de información dentro de su estructura||
|queryFile|string|||la ruta de acceso de archivo de consulta de sql de una visión general detalles y el nombre de archivo relativa a la ubicación de package.json||
|etiqueta|objeto JSON|||propiedad obligatoria para definir cada artículo de línea en la vista de lista de resumen|en el futuro, el nombre de esta propiedad para cambiar al igual que 'summaryList'|
|icono|string|||indicar el nombre del icono para lectura para cada elemento de vista de lista de resumen.|se documentarán lista (tbd) de iconos compatibles|
|column|string|||indicar el nombre de la primera columna de la vista de lista de resumen en el conjunto de resultados de consulta|en el futuro se cambiará el nombre de esta propiedad a un nombre más intuitivo|
|value|string|||indicar el nombre de la segunda columna de la vista de lista de resumen en el conjunto de resultados de consulta. El valor de esta columna se utiliza para comprobar las condiciones y establezca el color de punto de color de cada lista de resumen ver elementos|en el futuro se cambiará el nombre de esta propiedad en algo más intuitivo|
|condición|objeto JSON|||define la comprobación de la condición para el valor de la columna y determinar el color para cada elemento de vista de lista de resumen||
|if|string|siempre, igual a, valores, greaterThan, lessThan, greaterThanOrEqauls, lessThanOrEquals||operador de comprobación de condición|en el futuro se cambiará el nombre de propiedad al operador|
|equals|string|||valor de comprobación de condición|en el futuro cambiará este nombre de propiedad en 'value'|

## <a name="insight-actions"></a>Acciones de una perspectiva
Con un widget de una visión general y detalles de una visión general, pueden quedarse fácilmente un plan de acción para mitigar un problema o administrar. Por ejemplo, se considere ejecutar DBCC CHECKDB, leer registros de error o restaurar la base de datos cuando una base de datos está en una recuperación pendiente. O bien, puede ser cualquiera de las acciones que desea realizar.

Con [!INCLUDE[name-sos](../includes/name-sos-short.md)]de configuración de acciones de una perspectiva, puede asignar un acciones integradas como restaurar o aportar su propia acción definida con una secuencia de comandos de sql.

> Configuración de acciones personalizadas mediante la secuencia de comandos sql está en desarrollo y todavía no está disponible en la compilación de vista previa privada.

## <a name="sample-insight-action-definition"></a>Definición de acción de una visión general de ejemplo

```"actions"{}```define una acción de una perspectiva. Acción puede definirse en un ámbito específico como ```"server"```, ```"database"``` y así sucesivamente y [!INCLUDE[name-sos](../includes/name-sos-short.md)] pasa la información de contexto de conexión actual a la acción. 

Por ejemplo, cuando se inicia la acción de restauración para base de datos WideWorldImporters ```"database": "${Database}"``` definición indica que se pase ```Database``` valor de columna en el resultado de la consulta a la acción de restauración. A continuación, restaure el inicio de una acción para la base de datos. ```"types"```es una matriz json y varias acciones pueden mostrarse en la matriz. Básicamente se convierte en un menú contextual en el cuadro de diálogo Detalles de la información que el usuario puede haga clic en y realice la acción. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)]vista previa 0.17.1 ha habilitado la "copia de seguridad", "restaurar", "nueva consulta" y "nuevas bases de datos" como tipos de acción.

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```
