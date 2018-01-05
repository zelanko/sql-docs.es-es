---
title: "Tutorial: Habilitar el widget de una visión general de ejemplo de tabla espacio en uso en operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft"
description: "Este tutorial muestra cómo habilitar el widget de una visión general de ejemplo de tabla espacio en uso en el panel de la base de datos de las operaciones de SQL Studio (versión preliminar)."
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
ms.openlocfilehash: 7c51c7d1804baa490e665d316a08d911038c9f11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Tutorial: Habilitar la tabla espacio uso muestra una visión general widget mediante[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Este tutorial muestra cómo habilitar un widget de información en el panel de base de datos, proporcionando una vista de un vistazo sobre el uso de espacio para todas las tablas de una base de datos. Durante este tutorial, aprenderá cómo:

> [!div class="checklist"]
> * Activar rápidamente un widget de información con un ejemplo de widget de información integrada
> * Ver los detalles de uso del espacio de tabla
> * Filtrar los datos y ver detalles de etiqueta en un gráfico de una perspectiva

## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere SQL Server o base de datos de SQL Azure *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar mediante la base de datos de SQL Azure[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Activar una visión de administración en [!INCLUDE[name-sos](../includes/name-sos-short.md)]del panel base de datos
[!INCLUDE[name-sos](../includes/name-sos-short.md)]tiene un widget de ejemplo integrados para supervisar el espacio usado por las tablas en una base de datos.

1. Abra **configuración de usuario** presionando **Ctrl + Mayús + P** para abrir *comando paleta*, tipo *configuración* en el cuadro de búsqueda y seleccione  **Preferencias: Abra la configuración del usuario**.

   ![Comandos de configuración de usuario abierto](./media/tutorial-table-space-sql-server/open-user-settings.png)

2. Tipo de *panel* en búsqueda de configuraciones de cuadro de entrada y busque **dashboard.database.widgets**.

   ![Configuración de búsqueda](./media/tutorial-table-space-sql-server/search-settings.png)

3. Para personalizar el **dashboard.database.widgets** configuración, mantenga el mouse sobre el icono de lápiz a la izquierda de la **dashboard.database.widgets** texto, haga clic en **editar**  >  **Copia a la configuración de**.

4. Usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]de insight las opciones de IntelliSense, configurar *nombre* para el título del widget, *gridItemConfig* para el tamaño de widget, y *widget* seleccionando **tabla-espacio-db-insight** en la lista desplegable como se muestra en la captura de pantalla siguiente:

   ![Configuración de información](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Presione **CTRL+s** para guardar la configuración.

6. Panel Abrir base de datos haciendo clic en **TutorialDB** y haga clic en **administrar**.

   ![Abra panel](./media/tutorial-table-space-sql-server/insight-open-dashboard.png)

7. Vista *espacio usado por las tablas* tal y como se muestra en la captura de pantalla siguiente: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Trabajar con el gráfico de información

[!INCLUDE[name-sos](../includes/name-sos-short.md)]del gráfico de información proporciona detalles de filtrado y de desplazamiento del mouse. Para probar los siguientes pasos:

1. Haga clic en y activar o desactivar el *row_count* leyenda en el gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)]muestra y oculta la serie de datos como activar una leyenda o desactivar.
    
2. Desplace el puntero del mouse sobre el gráfico. [!INCLUDE[name-sos](../includes/name-sos-short.md)]Para obtener más información acerca de la etiqueta de la serie de datos y su valor tal y como se muestra en la captura de pantalla siguiente se muestra.

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