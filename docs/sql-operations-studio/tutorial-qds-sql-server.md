---
title: "Tutorial: Ejemplo de consultas más lentas de habilitar los cinco widget - operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft"
description: "Este tutorial muestra cómo habilitar el widget de ejemplo de consultas más lentas cinco en el panel de base de datos."
ms.custom: tools|sos
ms.date: 11/16/2017
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
ms.openlocfilehash: fc30051dff2bef07ac3e7d06aa98d92d4e05e79e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Tutorial: Agregar la *cinco consultas más lentas* widget de ejemplo en el panel de la base de datos

Este tutorial muestra el proceso de agregar uno de [!INCLUDE[name-sos](../includes/name-sos-short.md)]de widgets integrados de ejemplo para la *panel base de datos* para ver rápidamente la cinco consultas más lentas de la base de datos. También aprenderá a ver los detalles de las consultas lentas y planes de consulta mediante [!INCLUDE[name-sos](../includes/name-sos-short.md)]de características. Durante este tutorial, aprenderá cómo:

> [!div class="checklist"]
> * Habilitar el almacén de consultas en una base de datos
> * Agregar un widget de insight pregenerado en el panel de la base de datos
> * Ver detalles acerca de las consultas más lentas de la base de datos
> * Ver planes de ejecución de consulta para las consultas de ejecución lenta

[!INCLUDE[name-sos](../includes/name-sos-short.md)]incluye varias una visión general widgets out-of-the-box. Este tutorial muestra cómo agregar la *consulta datos de almacén de base de datos información* widget, pero los pasos son básicamente las mismas para agregar cualquier widget.

## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere SQL Server o base de datos de SQL Azure *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar mediante la base de datos de SQL Azure[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Activar el almacén de consultas para la base de datos

El widget en este ejemplo requiere *almacén de consultas* esté habilitado ejecuta la siguiente instrucción de Transact-SQL (T-SQL) en la base de datos:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-an-insight-widget-to-your-database-dashboard"></a>Agregar un widget de información en el panel de la base de datos

Para agregar un widget de información al panel, edite el *dashboard.database.widgets* en su *configuración de usuario* archivo.

1. Abra *configuración de usuario* presionando **Ctrl + Mayús + P** para abrir el *comando paleta*.
2. Tipo de *configuración* en el cuadro de búsqueda y de los archivos de configuración disponibles, seleccione **preferencias: abrir la configuración de usuario**.

   ![Comandos de configuración de usuario abierto](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Tipo de *panel* en la búsqueda de configuración y busque **dashboard.database.widgets**.

   ![Configuración de búsqueda](./media/tutorial-qds-sql-server/search-settings.png)

3. Para personalizar el **dashboard.database.widgets** configuración, mantenga el mouse sobre el icono de lápiz a la izquierda de la **dashboard.database.widgets** texto, haga clic en **editar**  >  **Copia a la configuración de**.

4. Después de copiar la configuración de **dashboard.database.widgets**, coloque el cursor al final de la línea después del corchete de apertura, presione **ENTRAR**y agregue una llave de apertura similar al siguiente (la llave de cierre aparecerán automáticamente):

   ```json
   "dashboard.database.widgets": [
   {}
   ```
5. Con el cursor entre las llaves, presione **Ctrl+barra espaciadora** y seleccione **nombre**. 
6. Terminar de configurar el widget parece similar al siguiente:

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
        }
    ...
    ```

5. Presione **CTRL+s** guardar modificados **configuración de usuario**.

6. Abra la *panel base de datos* , vaya a **TutorialDB** en el *servidores* sidebar, menú contextual y seleccione **administrar**.

   ![Abra panel](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. El widget de información aparece en el panel: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Ver detalles de la información para obtener más información

1. Para ver información adicional sobre un widget de una perspectiva, haga clic en el botón de puntos suspensivos (**...** ) en la esquina superior derecha y, a continuación, seleccione **mostrar detalles**.
2. Para mostrar más detalles sobre un elemento, seleccione cualquier elemento de **datos del gráfico** lista.

   ![Cuadro de diálogo de detalle de una perspectiva](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Haga clic en **query_sql_txt** en **detalles de los elementos** y haga clic en **Copiar celda**.

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

5. Presione **CTRL+s** para guardar el archivo y cambie la extensión de archivo a *.sqlplan*. Para este tutorial, el nombre del archivo *slowquery.sqlplan*.

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