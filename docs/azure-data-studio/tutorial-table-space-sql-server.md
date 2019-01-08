---
title: 'Tutorial: Habilitar el widget de insight tabla ejemplo de uso de espacio'
titleSuffix: Azure Data Studio
description: Este tutorial muestra cómo habilitar el widget de insight tabla ejemplo de uso de espacio en el panel de la base de datos de Azure Data Studio.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ebd3b1af1bc9b342ad6b2d33596e69b487888ced
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030359"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Tutorial: Habilitar la tabla espacio en uso muestra insight widget mediante [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Este tutorial muestra cómo habilitar un widget de información en el panel de la base de datos, que proporciona una vista de un vistazo sobre el uso de espacio para todas las tablas de una base de datos. Durante este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Activar rápidamente un widget de información mediante un ejemplo del widget de información integrada
> * Ver los detalles de uso del espacio de tabla
> * Filtrar los datos y ver los detalles de etiqueta en un gráfico insight

## <a name="prerequisites"></a>Requisitos previos

Este tutorial requiere SQL Server o Azure SQL Database *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar con SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar con Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Activar la información de administración en [!INCLUDE[name-sos](../includes/name-sos-short.md)]del panel de la base de datos
[!INCLUDE[name-sos](../includes/name-sos-short.md)] tiene un widget de ejemplo integrados para supervisar el espacio usado por las tablas en una base de datos.

1. Abra *configuración de usuario* presionando **Ctrl + Mayús + P** para abrir el *paleta de comandos*.
2. Tipo *configuración* en el cuadro de búsqueda y seleccione **preferencias: Abrir configuración de usuario**.
2. Tipo *panel* en búsqueda de la configuración del cuadro de entrada y busque **dashboard.database.widgets**.

3. Para personalizar el **dashboard.database.widgets** configuración que deba editar la **dashboard.database.widgets** entrada en el **configuración de usuario** sección (la columna en la lado derecho). Si no hay ningún **dashboard.database.widgets** en el **configuración de usuario** sección, mantenga el mouse sobre el **dashboard.database.widgets** texto en la columna de la configuración predeterminada y haga clic en el icono de lápiz que aparece a la izquierda del texto y haga clic en **copia a la configuración de**. Si indica que el elemento emergente **reemplazar en la configuración de**, no haga clic en él. Vaya a la **configuración de usuario** columna a la derecha y busque el **dashboard.database.widgets** sección y avance al paso siguiente.

4. En el **dashboard.database.widgets** sección, agregue lo siguiente:

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```
El **dashboard.database.widgets** sección debe ser similar a la imagen siguiente:

   ![Configuración de búsqueda](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Presione **CTRL+s** para guardar la configuración.

6. Panel de la base de datos abierta con el botón secundario **TutorialDB** y haga clic en **administrar**.

7. Ver el *espacio de tablas* widget de insight como se muestra en la siguiente imagen: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Trabajar con el gráfico insight

[!INCLUDE[name-sos](../includes/name-sos-short.md)]del gráfico de información proporciona detalles de filtrado y el desplazamiento del mouse. Para probar los pasos siguientes:

1. Haga clic en y activar o desactivar el *row_count* leyenda en el gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] muestra y oculta la serie de datos como una leyenda activa o desactivar.
    
2. Mantenga el puntero del mouse sobre el gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] Para obtener más información acerca de la etiqueta de serie de datos y su valor como se muestra en la captura de pantalla siguiente se muestra.

   ![la leyenda y la alternancia de gráfico](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido a:
> [!div class="checklist"]
> * Activar rápidamente un widget de información mediante una muestra del widget insight integrados.
> * Ver los detalles de uso del espacio de tabla.
> * Filtrar los datos y ver los detalles de etiqueta en un gráfico insight

Para obtener información sobre cómo crear un widget de datos personalizados, complete el tutorial siguiente:

> [!div class="nextstepaction"]
> [Crear un widget personalizado insight](tutorial-build-custom-insight-sql-server.md).
