---
title: Obtener acceso rápidamente a información y tareas comunes en Azure Data Studio | Microsoft Docs
description: Obtenga información acerca de cómo mostrar widgets precisos en Azure Data Studio.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: b163d110353d07811f0feb991772c90053651659
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356198"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>Paneles en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Para ver un panel, con el botón secundario en un servidor o base de datos y seleccione **administrar**.

![Panel de ejemplo](media/dashboards/sample-dashboard.png)

**Propiedades del servidor** contiene las propiedades del servidor, incluida la versión, edición, nombre de equipo y versión del sistema operativo.

**Tareas** contiene tareas commons como nueva consulta y de restauración.

**Buscar bases de datos** buscar fácilmente bases de datos existentes almacenados en el servidor, incluidas las tablas.

**Estado de copia de seguridad** buscar fácilmente el estado de copia de seguridad de bases de datos existentes.

## <a name="configuring-insight-widgets"></a>Configuración de Widgets de datos
Se recomienda encarecidamente que siga el tutorial para configurar el panel, que puede encontrarse [aquí](tutorial-build-custom-insight-sql-server.md).

Además, asegúrese de consultar la [procedimientos sobre la configuración de widgets de datos]().

Después de seguir este tutorial, siga leyendo para obtener más información sobre los widgets específicos que no están cubiertos en el tutorial.

## <a name="insight-detail"></a>Detalle de información
El control flotante detalles de información proporciona información más detallada de un widget de información relacionados. 
- Un widget de Insight representa una vista de resumen de un vistazo con recuento, línea, etcetera de gráfico. 
- El control flotante detalles de información proporciona detalles "explorar", mostrar información más detallada sobre los datos para cada elemento aparece en el widget de información de alto nivel. 
  - El contenido del control flotante de detalles se define con una consulta independiente de SQL para consultar del widget principal. 

No es necesario para una consulta de detalles de Insight conjunto, pero el diseño es estándar.
- La mitad superior de la vista siempre es una vista "Resumen" 2 columnas. Para usar las columnas que se definen mediante las propiedades "label" y "value" de la configuración de JSON
- Al hacer clic en una fila en la tabla de resumen, la parte inferior la mitad de la ventana flotante enumerará el conjunto completo de información de columna para esa fila.

### <a name="insight-detail-configuration-in-packagejson"></a>Configuración de detalle de Insight en package.json

Ejemplo de configuración de control flotante Insight detalles
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
|queryFile|string|||la ruta de acceso de archivo de consulta de sql de insight detalle y el nombre de archivo relativa a la ubicación de package.json||
|etiqueta|objeto JSON|||propiedad obligatoria para definir cada elemento de línea en la vista de lista de resumen|en el futuro, el nombre de esta propiedad para cambiar al igual que 'summaryList'|
|icono|string|||indicar el nombre del icono para lectura para cada elemento de vista de lista de resumen.|se documentará lista (tbd) de los iconos compatibles|
|column|string|||indicar el nombre de la primera columna en la vista de lista de resumen del conjunto de resultados de consulta|en el futuro se cambiará el nombre de esta propiedad en un nombre más intuitivo|
|value|string|||indicar el nombre de la segunda columna en la vista de lista de resumen del conjunto de resultados de consulta. El valor de esta columna se usa para comprobar las condiciones y establezca el color de punto de color de cada elementos vista de lista de resumen|en el futuro se cambiará el nombre de esta propiedad en algo más intuitivo|
|condición|objeto JSON|||define la comprobación de condición de valor de la columna y determinar el color de cada elemento de vista de lista de resumen||
|if|string|siempre, equals, notEquals, greaterThan, lessThan, greaterThanOrEqauls, lessThanOrEquals||operador de comprobación de condición|en el futuro se cambiará el nombre de propiedad al operador|
|equals|string|||valor de comprobación de condición|en el futuro cambiará el nombre de esta propiedad en 'value'|

## <a name="insight-actions"></a>Acciones de Insight
Con un widget de información y detalles de insight, fácilmente pueden proceder de un plan de acción para mitigar un problema o administrar. Por ejemplo, se considere ejecutar DBCC CHECKDB, leer los registros de error o restaurar la base de datos cuando una base de datos está en una recuperación pendiente. O puede ser cualquiera de las acciones que desea realizar.

Uso de [!INCLUDE[name-sos](../includes/name-sos-short.md)]de configuración de acciones de Insight, puede asignar un acciones integradas, como restaurar o traiga su propia acción definida con una secuencia de comandos sql.

> Configuración de acciones personalizadas mediante script de sql está en desarrollo y aún no está disponible en la compilación de versión preliminar privada.

## <a name="sample-insight-action-definition"></a>Definición de la acción de la información de ejemplo

```"actions"{}``` define una acción de insight. Acción puede definirse a través de un ámbito específico, como ```"server"```, ```"database"``` y así sucesivamente y [!INCLUDE[name-sos](../includes/name-sos-short.md)] pasa la información de contexto de conexión actual a la acción. 

Por ejemplo, cuando se inicia la acción de restauración de base de datos WideWorldImporters, ```"database": "${Database}"``` definición indica que se pase ```Database``` valor de columna en el resultado de la consulta a la acción de restauración. A continuación, restaure el inicio de una acción para la base de datos. ```"types"``` es una matriz json y pueden aparecer varias acciones en la matriz. Básicamente, se convierte en un menú contextual en el cuadro de diálogo Detalles de la información que el usuario puede haga clic en y realice la acción. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] vista previa 0.17.1 habilitó "backup", "restore", "nueva consulta" y "nueva-base de datos" como tipos de acción.

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
