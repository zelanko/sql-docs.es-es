---
title: 'Tutorial: Ejemplo de consultas más lentas de habilitar los cinco widget - operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft'
description: Este tutorial muestra cómo habilitar el widget de ejemplo de consultas más lentas cinco en el panel de base de datos.
ms.custom: tools|sos
ms.date: 03/15/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.openlocfilehash: d06bd752b0cdd07d87d8e5816a74d6e2d43d31ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Agregar la *cinco consultas más lentas* widget de ejemplo en el panel de la base de datos

Este tutorial muestra el proceso de agregar uno de [!INCLUDE[name-sos](../includes/name-sos-short.md)]de widgets integrados de ejemplo para la *panel base de datos* para ver rápidamente la cinco consultas más lentas de la base de datos. También aprenderá a ver los detalles de las consultas lentas y planes de consulta mediante [!INCLUDE[name-sos](../includes/name-sos-short.md)]de características. Durante este tutorial, aprenderá cómo:

> [!div class="checklist"]
> * Habilitar el almacén de consultas en una base de datos
> * Agregar un widget de insight pregenerado en el panel de la base de datos
> * Ver detalles acerca de las consultas más lentas de la base de datos
> * Ver planes de ejecución de consulta para las consultas de ejecución lenta

[!INCLUDE[name-sos](../includes/name-sos-short.md)] incluye varias una visión general widgets out-of-the-box. Este tutorial muestra cómo agregar la *consulta datos de almacén de base de datos información* widget, pero los pasos son básicamente las mismas para agregar cualquier widget.

## <a name="prerequisites"></a>Requisitos previos

Este tutorial requiere SQL Server o base de datos de SQL Azure *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar mediante la base de datos de SQL Azure [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Activar el almacén de consultas para la base de datos

El widget en este ejemplo requiere *almacén de consultas* esté habilitado.

1. Haga clic con el **TutorialDB** base de datos (en el **servidores** sidebar) y seleccione **nueva consulta**.
2. Pegue la siguiente instrucción de Transact-SQL (T-SQL) en el editor de consultas y haga clic en **ejecutar**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Agregar el widget de consultas de ejecución lenta en el panel de la base de datos

Para agregar el *ralentizar el widget de consultas* al panel, editar la *dashboard.database.widgets* en su *configuración de usuario* archivo.

1. Abra *configuración de usuario* presionando **Ctrl + Mayús + P** para abrir el *comando paleta*.
2. Tipo de *configuración* en el cuadro de búsqueda y seleccione **preferencias: abrir la configuración de usuario**.

   ![Comandos de configuración de usuario abierto](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Tipo de *panel* en la búsqueda de configuración y busque **dashboard.database.widgets**.

   ![Configuración de búsqueda](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar el **dashboard.database.widgets** configuración es necesario editar el **dashboard.database.widgets** entrada en el **configuración de usuario** sección (la columna en la (derecha). Si no hay ningún **dashboard.database.widgets** en el **configuración de usuario** sección, mantenga el mouse sobre la **dashboard.database.widgets** texto en la columna de la configuración predeterminada y haga clic en el icono de lápiz situado a la izquierda del texto y haga clic en **copia a la configuración de**. Si el elemento emergente indica **reemplazar en la configuración de**, no haga clic en él. Vaya a la **configuración de usuario** columna a la derecha y busque la **dashboard.database.widgets** sección y avanzar al paso siguiente.

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

1. Presione **CTRL+s** guardar modificados **configuración de usuario**.

6. Abra la *panel base de datos* , vaya a **TutorialDB** en el **servidores** sidebar, menú contextual y seleccione **administrar**.

   ![Abra panel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. El widget de información aparece en el panel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Ver detalles de la información para obtener más información

1. Para ver información adicional sobre un widget de una perspectiva, haga clic en el botón de puntos suspensivos (**...** ) en la esquina superior derecha y, a continuación, seleccione **mostrar detalles**.
2. Para mostrar más detalles sobre un elemento, seleccione cualquier elemento de **datos del gráfico** lista.

   ![Cuadro de diálogo de detalle de una perspectiva](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Haga clic en la celda situada a la derecha del **query_sql_txt** en **detalles de los elementos** y haga clic en **Copiar celda**.

4. Cerrar la **visión** panel.

## <a name="view-the-query-plan"></a>Ver el plan de consulta 

1. Abra un nuevo editor de consultas presionando **CTRL+n**.

2. Pegue el texto de consulta de los pasos anteriores en el editor.

3. Haga clic en **explican**.

   ![Explica una visión general QDS](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Ver el plan de ejecución de la consulta:

   ![plan de presentación](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Guardar y abrir un plan de consulta 

1. Abra el cuadro de diálogo de detalles de una perspectiva.
2. Seleccione uno de los elementos de la consulta.
2. Haga clic en **query_plan** valor y seleccione **Copiar celda**

   ![Visión QDS plan](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Presione **CTRL+n** para abrir un nuevo editor.

4. Pegue el plan copiado en el editor.

5. Presione **CTRL+s** para guardar el archivo y cambie la extensión de archivo a *.sqlplan*. *SQLPlan* no aparece en la lista desplegable la extensión de archivo, por lo que simplemente escríbalo en. Para este tutorial, el nombre del archivo *slowquery.sqlplan*.

6. El plan de consulta se abre en [!INCLUDE[name-sos](../includes/name-sos-short.md)]del Visor del plan de consulta:

   ![Visión QDS plan](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Habilitar el almacén de consultas en una base de datos
> * Agregar un widget de información en el panel de la base de datos
> * Ver detalles acerca de las consultas más lentas de la base de datos
> * Ver planes de ejecución de consulta para las consultas de ejecución lenta


Para obtener información sobre cómo habilitar la **uso del espacio de tabla** una visión general de ejemplo, siga el tutorial siguiente:

> [!div class="nextstepaction"]
> [Habilitar el widget de una visión general del ejemplo de espacio de tabla](tutorial-table-space-sql-server.md)