---
title: 'Tutorial: Compilación de un widget de datos personalizados en Azure Data Studio | Microsoft Docs'
description: Este tutorial muestra cómo compilar widgets de datos personalizados y agregarlos a los paneles de base de datos y servidor en Azure Data Studio.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d14c8d9e4a17782464e13b380334c85c9ee1036c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "48039099"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Tutorial: Compilación de un widget de datos personalizados

Este tutorial muestra cómo usar sus propias consultas insight para compilar widgets de datos personalizado.

Durante este tutorial obtendrá información sobre cómo:
> [!div class="checklist"]
> * Ejecute su propia consulta y verlo en un gráfico
> * Crear un widget de datos personalizados en el gráfico
> * Agregue el gráfico a un panel de servidor o base de datos
> * Agregar detalles para el widget de datos personalizados

## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere SQL Server o Azure SQL Database *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar con SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar con Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>Ejecutar su propia consulta y ver el resultado en una vista de gráfico
En este paso, ejecutará una secuencia de comandos sql para consultar las sesiones activas actuales.

1. Para abrir un nuevo editor, presione **CTRL+n**. 

2. Cambiar el contexto de conexión a **TutorialDB**.

3. Pegue la siguiente consulta en el editor de consultas:

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. Guarde la consulta en el editor para un \*archivo .sql. Para este tutorial, guarde el script como *activeSession.sql*.

5. Para ejecutar la consulta, presione **F5**.

6. Después de que se muestran los resultados de consulta, haga clic en **vista como gráfico**, a continuación, haga clic en el **Visor gráfico** ficha.

7. Cambio **tipo de gráfico** a **recuento**. Estos valores representan un gráfico de recuento.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Agregue la información personalizada en el panel de la base de datos

1. Para abrir la configuración del widget insight, haga clic en **crear Insight** en *Visor gráfico*:

   ![configuración](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Copie la configuración de información (los datos JSON). 

3. Presione **CTRL+coma** para abrir *configuración de usuario*.

4. Tipo *panel* en *configuración de búsqueda*.

5. Haga clic en **editar** para *dashboard.database.widgets*.

   ![configuración del panel](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Pegue la configuración de la información JSON en *dashboard.database.widgets*. Base de datos panel configuración es similar al siguiente:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. Guardar el *configuración de usuario* de archivo y abra el *TutorialDB* panel de la base de datos para ver el widget de sesiones activas:

   ![activesession insight](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Agregar detalles a los datos personalizados

1. Para abrir un nuevo editor, presione **CTRL+n**.

2. Cambiar el contexto de conexión a **TutorialDB**.

3. Pegue la siguiente consulta en el editor de consultas:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Guarde la consulta en el editor para un \*archivo .sql. Para este tutorial, guarde el script como *activeSessionDetail.sql*.

5. Presione **CTRL+coma** para abrir *configuración de usuario*.

6. Editar las existentes *dashboard.database.widgets* nodo en el archivo de configuración:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. Guardar el *configuración de usuario* de archivo y abra el *TutorialDB* panel base de datos. Haga clic en el botón de puntos suspensivos (...) junto a *mi Widget* para mostrar los detalles:

    ![activesession insight](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Ejecute su propia consulta y verlo en un gráfico
> * Crear un widget de datos personalizados en el gráfico
> * Agregue el gráfico a un panel de servidor o base de datos
> * Agregar detalles para el widget de datos personalizados

Para obtener información sobre copias de seguridad y restaurar bases de datos, complete el tutorial siguiente:

> [!div class="nextstepaction"]
> [Copia de seguridad y restaurar bases de datos](tutorial-backup-restore-sql-server.md).
