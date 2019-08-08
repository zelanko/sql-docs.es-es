---
title: 'Tutorial: Habilitar el widget de ejemplo de cinco consultas más lentas'
titleSuffix: Azure Data Studio
description: En este tutorial se muestra cómo habilitar el widget de ejemplo de cinco consultas más lentas en el panel de base de datos.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 5c94d2cf8b80ad7724cc1f710dc67d3f4a13c59e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959066"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Agregar el widget de ejemplo *cinco consultas más lentas* al panel de base de datos

En este tutorial se muestra el proceso de incorporación de uno de los widgets de ejemplo integrados de [!INCLUDE[name-sos](../includes/name-sos-short.md)] al *panel de base de datos* para ver rápidamente las cinco consultas más lentas de una base de datos. También se aprende a ver los detalles de las consultas lentas y los planes de consulta mediante características de [!INCLUDE[name-sos](../includes/name-sos-short.md)]. En este tutorial se aprende a:

> [!div class="checklist"]
> * Habilitar Almacén de consultas en una base de datos
> * Agregar un widget de información previamente integrado al panel de base de datos
> * Ver detalles sobre las consultas más lentas de la base de datos
> * Ver planes de ejecución de consulta para las consultas lentas

[!INCLUDE[name-sos](../includes/name-sos-short.md)] incluye varios widgets de información listos para usar. En este tutorial se muestra cómo agregar el widget *query-data-store-db-insight*, pero los pasos son básicamente los mismos para agregar cualquier widget.

## <a name="prerequisites"></a>Prerequisites

En este tutorial se requiere la instancia de SQL Server o Azure SQL Database *TutorialDB*. Para crear la base de datos *TutorialDB*, complete alguno de los siguientes inicios rápidos:

- [Conectarse y consultar con [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Use [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] para conectarse y consultar la base de datos SQL de Azure](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Activar Almacén de consultas para la base de datos

El widget de este ejemplo requiere que *Almacén de consultas* esté habilitado.

1. Haga clic con el botón derecho en la base de datos **TutorialDB** (en la barra lateral **SERVIDORES**) y seleccione **Nueva consulta**.
2. Pegue la siguiente instrucción de Transact-SQL (T-SQL) en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Agregar el widget de consultas lentas al panel de base de datos

Para agregar el *widget de consultas lentas* al panel, edite el valor *dashboard.database.widgets* del archivo *Configuración de usuario*.

1. Abra *Configuración de usuario* al presionar **Ctrl + Mayús + P** para abrir la *paleta de comandos*.
2. Escriba *configuración* en el cuadro de búsqueda y seleccione **Preferencias: Abrir configuración de usuario**.

   ![Comando Abrir configuración de usuario](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Escriba *dashboard* en el cuadro de búsqueda de configuración y busque **dashboard.database.widgets**.

   ![Búsqueda de configuración](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar la configuración de **dashboard.database.widgets**, debe editar la entrada **dashboard.database.widgets** de la sección **CONFIGURACIÓN DE USUARIO** (la columna del lado derecho). Si **dashboard.database.widgets** no aparece en la sección **CONFIGURACIÓN DE USUARIO**, mantenga el mouse sobre el texto **dashboard.database.widgets** de la columna CONFIGURACIÓN PREDETERMINADA, haga clic en el icono de lápiz que aparece a la izquierda del texto y, luego, en **Copiar en Configuración**. Si el elemento emergente indica **Reemplazar en Configuración**, no haga clic en él. Vaya a la columna **CONFIGURACIÓN DE USUARIO** a la derecha, busque la sección **dashboard.database.widgets** y vaya al paso siguiente.

4. En la sección **dashboard.database.widgets**, agregue lo siguiente:

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

1. Si esta es la primera vez que agrega un widget nuevo, el aspecto de la sección **dashboard.database.widgets** debe ser similar al siguiente:

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

1. Presione **Ctrl + S** para guardar la **Configuración de usuario** modificada.

6. Abra el *panel de la base de datos* al ir a **TutorialDB** en la barra lateral **SERVIDORES**, hacer clic con el botón derecho y seleccionar **Administrar**.

   ![Apertura del panel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. El widget de información aparece en el panel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Ver detalles para obtener más información

1. Para ver información adicional de un widget de información, haga clic en los puntos suspensivos ( **...** ) de la esquina superior derecha y seleccione **Mostrar detalles**.
2. Para mostrar más detalles de un elemento, seleccione cualquier elemento de la lista **Datos de gráfico**.

   ![Cuadro de diálogo de detalles de Información](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Haga clic con el botón derecho en la celda situada a la derecha de **query_sql_txt** en **Detalles del elemento** y haga clic en **Copiar celda**.

4. Cierre el panel **Información**.

## <a name="view-the-query-plan"></a>Ver el plan de consulta 

1. Abra un nuevo editor de consultas al presionar **Ctrl + N**.

2. Pegue el texto de la consulta de los pasos anteriores en el editor.

3. Haga clic en **Explicar**.

   ![Explicación de QDS en Información](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Vea el plan de ejecución de la consulta:

   ![plan de presentación](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Guardar y abrir un plan de consulta 

1. Abra el cuadro de diálogo de detalles de Información.
2. Seleccione uno de los elementos de consulta.
2. Haga clic con el botón derecho en el valor **query_plan** y seleccione **Copiar celda**.

   ![Plan de QDS de Información](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Presione **Ctrl + N** para abrir un nuevo editor.

4. Pegue el plan copiado en el editor.

5. Presione **Ctrl + S** para guardar el archivo y cambie la extensión de archivo a *.sqlplan*. *.sqlplan* no aparece en la lista desplegable de extensiones de archivo, así que simplemente escríbala. En este tutorial, asigne al archivo el nombre *slowquery.sqlplan*.

6. El plan de consulta se abre en el visor de planes de consulta de [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

   ![Plan de QDS de Información](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido a realizar lo siguiente:
> [!div class="checklist"]
> * Habilitar Almacén de consultas en una base de datos
> * Agregar un widget de información al panel de base de datos
> * Ver detalles sobre las consultas más lentas de la base de datos
> * Ver planes de ejecución de consulta para las consultas lentas


Para obtener información sobre cómo habilitar la información de ejemplo de **uso de espacio de tabla**, complete el tutorial siguiente:

> [!div class="nextstepaction"]
> [Habilitar el widget de información de ejemplo de espacio de tabla](tutorial-table-space-sql-server.md)
