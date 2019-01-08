---
title: 'Tutorial: Habilitar el widget de ejemplo de las consultas más lentas cinco'
titleSuffix: Azure Data Studio
description: Este tutorial muestra cómo habilitar el widget de ejemplo de las consultas más lentas cinco en el panel de la base de datos.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 491e66ecc8b0dfb3024a2beb59cfefd3f8e0d28f
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030789"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Agregar el *cinco consultas más lentas* widget de ejemplo en el panel de la base de datos

Este tutorial muestra el proceso de agregar uno de [!INCLUDE[name-sos](../includes/name-sos-short.md)]de widgets de ejemplo integrados para el *panel base de datos* para ver rápidamente la cinco consultas más lentas de la base de datos. También aprenderá a ver los detalles de las consultas lentas y planes de consulta mediante [!INCLUDE[name-sos](../includes/name-sos-short.md)]de características. Durante este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Habilitar la consulta Store en una base de datos
> * Agregar un widget de insight creados previamente en el panel de la base de datos
> * Ver detalles acerca de las consultas más lentas de la base de datos
> * Ver planes de ejecución de consultas para las consultas lentas

[!INCLUDE[name-sos](../includes/name-sos-short.md)] incluye varias insight widgets-de-fábrica. Este tutorial muestra cómo agregar el *consulta-data-store-db-insight* widget, pero los pasos son básicamente las mismas para agregar cualquier widget.

## <a name="prerequisites"></a>Requisitos previos

Este tutorial requiere SQL Server o Azure SQL Database *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar con SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar con Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Activar la consulta Store para la base de datos

El widget en este ejemplo requiere *Query Store* esté habilitado.

1. Haga clic en el **TutorialDB** base de datos (en el **servidores** sidebar) y seleccione **nueva consulta**.
2. Pegue la siguiente instrucción de Transact-SQL (T-SQL) en el editor de consultas y haga clic en **ejecutar**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Agregar el widget de consultas lentas en el panel de la base de datos

Para agregar el *lenta widget consultas* al panel, edite el *dashboard.database.widgets* en su *configuración de usuario* archivo.

1. Abra *configuración de usuario* presionando **Ctrl + Mayús + P** para abrir el *paleta de comandos*.
2. Tipo *configuración* en el cuadro de búsqueda y seleccione **preferencias: Abrir configuración de usuario**.

   ![Comando de configuración de usuario abiertos](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Tipo *panel* en la búsqueda de configuración y busque **dashboard.database.widgets**.

   ![Configuración de búsqueda](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar el **dashboard.database.widgets** configuración que deba editar la **dashboard.database.widgets** entrada en el **configuración de usuario** sección (la columna en la lado derecho). Si no hay ningún **dashboard.database.widgets** en el **configuración de usuario** sección, mantenga el mouse sobre el **dashboard.database.widgets** texto en la columna de la configuración predeterminada y haga clic en el icono de lápiz que aparece a la izquierda del texto y haga clic en **copia a la configuración de**. Si indica que el elemento emergente **reemplazar en la configuración de**, no haga clic en él. Vaya a la **configuración de usuario** columna a la derecha y busque el **dashboard.database.widgets** sección y avance al paso siguiente.

4. En el **dashboard.database.widgets** sección, agregue lo siguiente:

   ```json
        {
            "name": "slow queries widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "query-data-store-db-insight": null
            }
        },
    ```

1. Si se trata de la primera vez que se agrega un nuevo widget, el **dashboard.database.widgets** sección debe ser similar al siguiente:

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

1. Presione **CTRL+s** guardar modificado **configuración de usuario**.

6. Abra el *panel base de datos* yendo a **TutorialDB** en el **servidores** sidebar, con el botón secundario y seleccione **administrar**.

   ![Abrir el panel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. El widget de información aparece en el panel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Ver detalles de la información para obtener más información

1. Para ver información adicional sobre un widget de información, haga clic en el botón de puntos suspensivos (**...** ) en la esquina superior derecha y seleccione **mostrar detalles**.
2. Para mostrar más detalles de un elemento, seleccione cualquier elemento **datos del gráfico** lista.

   ![Cuadro de diálogo de información](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Haga clic en la celda situada a la derecha del **query_sql_txt** en **detalles del elemento** y haga clic en **Copiar celda**.

4. Cerrar la **Insights** panel.

## <a name="view-the-query-plan"></a>Ver el plan de consulta 

1. Abra un nuevo editor de consultas presionando **CTRL+n**.

2. Pegue el texto de consulta de los pasos anteriores en el editor.

3. Haga clic en **explican**.

   ![Explique Insight QDS](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Ver plan de ejecución de la consulta:

   ![plan de presentación](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Guardar y abrir un plan de consulta 

1. Abra el cuadro de diálogo de información detallada.
2. Seleccione uno de los elementos de la consulta.
2. Haga clic en **query_plan** valor y seleccione **Copiar celda**

   ![Plan de Insights QDS](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Presione **CTRL+n** para abrir un nuevo editor.

4. Pegue el plan copiado en el editor.

5. Presione **CTRL+s** para guardar el archivo y cambie la extensión de archivo a *.sqlplan*. *.sqlplan* no aparece en la lista desplegable de extensión de archivo, así que escriba. Para este tutorial, el nombre del archivo *slowquery.sqlplan*.

6. El plan de consulta se abre en [!INCLUDE[name-sos](../includes/name-sos-short.md)]del Visor del plan de consulta:

   ![Plan de Insights QDS](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido a:
> [!div class="checklist"]
> * Habilitar la consulta Store en una base de datos
> * Agregar un widget de información en el panel de la base de datos
> * Ver detalles acerca de las consultas más lentas de la base de datos
> * Ver planes de ejecución de consultas para las consultas lentas


Para obtener información sobre cómo habilitar el **uso del espacio de tabla** datos de ejemplo, completar el tutorial siguiente:

> [!div class="nextstepaction"]
> [Habilitar el widget de insight de ejemplo de espacio de tabla](tutorial-table-space-sql-server.md)
