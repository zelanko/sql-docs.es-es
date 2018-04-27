---
title: 'Tutorial: Habilitar el widget de una visión general de ejemplo de tabla espacio en uso en operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft'
description: Este tutorial muestra cómo habilitar el widget de una visión general de ejemplo de tabla espacio en uso en el panel de la base de datos de las operaciones de SQL Studio (versión preliminar).
ms.custom: tools|sos
ms.date: 03/19/2018
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
ms.workload: Inactive
ms.openlocfilehash: 6ec260eb6c82bfcac0e38251375fc9b58af55db1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Tutorial: Habilitar la tabla espacio uso muestra una visión general widget mediante [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Este tutorial muestra cómo habilitar un widget de información en el panel de base de datos, proporcionando una vista de un vistazo sobre el uso de espacio para todas las tablas de una base de datos. Durante este tutorial, aprenderá cómo:

> [!div class="checklist"]
> * Activar rápidamente un widget de información con un ejemplo de widget de información integrada
> * Ver los detalles de uso del espacio de tabla
> * Filtrar los datos y ver detalles de etiqueta en un gráfico de una perspectiva

## <a name="prerequisites"></a>Requisitos previos

Este tutorial requiere SQL Server o base de datos de SQL Azure *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar mediante la base de datos de SQL Azure [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Activar una visión de administración en [!INCLUDE[name-sos](../includes/name-sos-short.md)]del panel base de datos
[!INCLUDE[name-sos](../includes/name-sos-short.md)] tiene un widget de ejemplo integrados para supervisar el espacio usado por las tablas en una base de datos.

1. Abra *configuración de usuario* presionando **Ctrl + Mayús + P** para abrir el *comando paleta*.
2. Tipo de *configuración* en el cuadro de búsqueda y seleccione **preferencias: abrir la configuración de usuario**.
2. Tipo de *panel* en búsqueda de configuraciones de cuadro de entrada y busque **dashboard.database.widgets**.

3. Para personalizar el **dashboard.database.widgets** configuración es necesario editar el **dashboard.database.widgets** entrada en el **configuración de usuario** sección (la columna en la (derecha). Si no hay ningún **dashboard.database.widgets** en el **configuración de usuario** sección, mantenga el mouse sobre la **dashboard.database.widgets** texto en la columna de la configuración predeterminada y haga clic en el icono de lápiz situado a la izquierda del texto y haga clic en **copia a la configuración de**. Si el elemento emergente indica **reemplazar en la configuración de**, no haga clic en él. Vaya a la **configuración de usuario** columna a la derecha y busque la **dashboard.database.widgets** sección y avanzar al paso siguiente.

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

6. Panel Abrir base de datos haciendo clic en **TutorialDB** y haga clic en **administrar**.

7. Ver el *espacio de tabla* widget de información tal como se muestra en la siguiente imagen: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Trabajar con el gráfico de información

[!INCLUDE[name-sos](../includes/name-sos-short.md)]del gráfico de información proporciona detalles de filtrado y de desplazamiento del mouse. Para probar los siguientes pasos:

1. Haga clic en y activar o desactivar el *row_count* leyenda en el gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] muestra y oculta la serie de datos como activar una leyenda o desactivar.
    
2. Desplace el puntero del mouse sobre el gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] Para obtener más información acerca de la etiqueta de la serie de datos y su valor tal y como se muestra en la captura de pantalla siguiente se muestra.

   ![alternancia de gráfico y la leyenda](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Encienda rápidamente un widget de información con una muestra de widget de información integrada.
> * Ver los detalles de uso del espacio de tabla.
> * Filtrar los datos y ver detalles de etiqueta en un gráfico de una perspectiva

Para obtener información sobre cómo crear un widget de información personalizada, realice el siguiente tutorial:

> [!div class="nextstepaction"]
> [Crear un widget de información personalizada](tutorial-build-custom-insight-sql-server.md).