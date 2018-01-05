---
title: "Tutorial: Crear un widget de información personalizada en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft"
description: "Este tutorial muestra cómo compilar widgets de insight personalizados y agregarlos a los paneles de base de datos y el servidor en las operaciones de SQL Studio (versión preliminar)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 344cf021a4a0abc13fc8c531875c604095c8c0d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Tutorial: Crear un widget de información personalizada

Este tutorial muestra cómo usar sus propias consultas de una perspectiva para compilar widgets de información personalizada.

Durante este tutorial aprenderá cómo:
> [!div class="checklist"]
> * Ejecutar su propia consulta y ver en un gráfico
> * Crear un widget de información personalizada del gráfico
> * Agregue el gráfico a un panel de servidor o base de datos
> * Agregar detalles para el widget de información personalizada

## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere SQL Server o base de datos de SQL Azure *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar mediante la base de datos de SQL Azure[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


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

4. Guardar la consulta en el editor para un \*archivo .sql. Para este tutorial, guarde el script como *activeSession.sql*.

5. Para ejecutar la consulta, presione **F5**.

6. Cuando se muestren los resultados de la consulta, haga clic en **vista como gráfico**, a continuación, haga clic en el **Visor gráfico** ficha.

7. Cambio **tipo de gráfico** a **recuento**. Estos valores representan un gráfico de recuento.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Agregar la información personalizada en el panel de la base de datos

1. Para abrir la configuración del widget una visión general, haga clic en **crear una perspectiva** en *Visor gráfico*:

   ![configuración](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Copie la configuración de visión (los datos JSON). 

3. Presione **CTRL+coma** para abrir *configuración de usuario*.

4. Tipo de *panel* en *configuración de búsqueda*.

5. Haga clic en **editar** para *dashboard.database.widgets*.

   ![Configuración del panel](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Pegue la configuración de una perspectiva JSON en *dashboard.database.widgets*. Base de datos panel configuración es similar al siguiente:

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

7. Guardar el *configuración de usuario* de archivos y abrir el *TutorialDB* panel de base de datos para ver el widget de sesiones activas:

   ![Visión general de activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Agregar detalles a información personalizada

1. Para abrir un nuevo editor, presione **CTRL+n**.

2. Cambiar el contexto de conexión a **TutorialDB**.

3. Pegue la siguiente consulta en el editor de consultas:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Guardar la consulta en el editor para un \*archivo .sql. Para este tutorial, guarde el script como *activeSessionDetail.sql*.

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

7. Guardar el *configuración de usuario* de archivos y abrir el *TutorialDB* panel base de datos. Haga clic en el botón de puntos suspensivos (...) junto a *mi Widget* para mostrar los detalles:

    ![Visión general de activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Ejecutar su propia consulta y ver en un gráfico
> * Crear un widget de información personalizada del gráfico
> * Agregue el gráfico a un panel de servidor o base de datos
> * Agregar detalles para el widget de información personalizada

Para obtener información sobre copias de seguridad y restaurar bases de datos, complete el tutorial siguiente:

> [!div class="nextstepaction"]
> [Copia de seguridad y restaurar bases de datos](tutorial-backup-restore-sql-server.md).