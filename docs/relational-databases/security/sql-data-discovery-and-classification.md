---
title: Clasificación y detección de datos de SQL | Microsoft Docs
description: Clasificación y detección de datos de SQL
services: sql-server
documentationcenter: ''
author: giladm
manager: shaik
ms.reviewer: carlrab
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-server
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 02/13/2018
ms.author: giladm
ms.openlocfilehash: eee9d5b920f422d000fa4e9cb8b78924cb55b466
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2018
---
# <a name="sql-data-discovery-and-classification"></a>Clasificación y detección de datos de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La clasificación y detección de datos cuenta con una nueva herramienta integrada en SQL Server Management Studio (SSMS) para **detectar**, **clasificar**, **etiquetar** & **notificar** los datos confidenciales de las bases de datos.
La detección y la clasificación de la información más confidencial (empresarial, financiera, sanitaria, personal, etc.) pueden desempeñar un papel fundamental en el estado de protección de la información de la organización. Puede servir como infraestructura para lo siguiente:
* Ayudar a cumplir los estándares de privacidad de datos y los requisitos de cumplimiento de normas, como RGPD.
* Controlar el acceso a bases de datos o columnas que contienen datos altamente confidenciales y aumentar su seguridad.


> [!NOTE]
> La clasificación y detección de datos es **compatible con SQL Server 2008 y versiones posteriores**. Para Azure SQL Database, vea [Clasificación y detección de datos de Azure SQL Database](https://go.microsoft.com/fwlink/?linkid=866265).

## <a id="subheading-1"></a>Información general
La clasificación y detección de datos incluye un conjunto de servicios avanzados que forman un nuevo paradigma de Information Protection de SQL destinado a proteger los datos, no solo la base de datos:
* **Detección y recomendaciones**: el motor de clasificación examina la base de datos e identifica las columnas que contienen datos potencialmente confidenciales. Después, proporciona una manera sencilla de revisar y aplicar las recomendaciones de clasificación apropiadas, así como de clasificar las columnas de forma manual.
* **Etiquetado**: las etiquetas de clasificación de confidencialidad se pueden etiquetar de forma persistente en columnas.
* **Visibilidad**: el estado de clasificación de la base de datos puede consultarse en un informe detallado que se puede imprimir o exportar para su uso con fines de cumplimiento y auditoría, así como para otras necesidades.

## <a id="subheading-2"></a>Detectar, clasificar y etiquetar columnas confidenciales
En la sección siguiente se describen los pasos necesarios para detectar, clasificar y etiquetar las columnas que contienen datos confidenciales en la base de datos, así como para ver el estado de clasificación actual de la base de datos y exportar informes.

La clasificación incluye dos atributos de metadatos:
* Etiquetas: son los atributos principales de clasificación, que se usan para definir el nivel de confidencialidad de los datos almacenados en la columna.  
* Tipos de información: proporcionan una granularidad adicional para el tipo de datos almacenados en la columna.

<br>
**Para clasificar la base de datos de SQL Server:**

1. En SQL Server Management Studio (SSMS), conéctese a SQL Server.

2. En el Explorador de objetos de SSMS, haga clic con el botón derecho en la base de datos que quiere clasificar y seleccione **Tareas** > **Classify Data…** (Clasificar datos…).

    ![Panel de navegación][1]

3. El motor de clasificación examina la base de datos en busca de columnas que contengan datos potencialmente confidenciales y proporciona una lista de **clasificaciones de columna recomendadas**:

    * Para ver la lista de clasificaciones de columna recomendadas, haga clic en el cuadro de notificación de recomendaciones en la parte superior o en el panel de recomendaciones en la parte inferior de la ventana:

        ![Panel de navegación][2]

        ![Panel de navegación][3]

    * Revise la lista de recomendaciones:
        * Para aceptar una recomendación para una columna específica, active la casilla en la columna izquierda de la fila correspondiente. También puede marcar *todas las recomendaciones* como aceptadas. Para ello, active la casilla del encabezado de la tabla de recomendaciones.

        * También puede cambiar el tipo de información y la etiqueta de confidencialidad recomendados mediante los cuadros desplegables.        

        ![Panel de navegación][4]

    * Para aplicar las recomendaciones seleccionadas, haga clic en el botón azul **Accept selected recommendations** (Aceptar recomendaciones seleccionadas).

        ![Panel de navegación][5]

4. También puede **clasificar manualmente** las columnas como alternativa a la clasificación basada en recomendaciones, o además de ella:

    * Haga clic en **Agregar clasificación** en el menú superior de la ventana.

        ![Panel de navegación][6]

    * En la ventana contextual que se abre, seleccione el esquema > tabla > columna que quiera clasificar, así como el tipo de información y la etiqueta de confidencialidad. Después, haga clic en el botón azul **Agregar clasificación** situado en la parte inferior de la ventana contextual.

        ![Panel de navegación][7]

5. Para completar la clasificación y etiquetar de forma persistente las columnas de la base de datos con los nuevos metadatos de clasificación, haga clic en **Guardar** en el menú superior de la ventana.

    ![Panel de navegación][8]


6. Para generar un informe con un resumen completo del estado de clasificación de la base de datos, haga clic en **Ver informe** en el menú superior de la ventana.

    ![Panel de navegación][9]

    ![Panel de navegación][10]


## <a id="subheading-3"></a>Pasos siguientes

Para Azure SQL Database, vea [Clasificación y detección de datos de Azure SQL Database](https://go.microsoft.com/fwlink/?linkid=866265).

Considere la posibilidad de proteger sus columnas confidenciales mediante la aplicación de mecanismos de seguridad en el nivel de columna:

* [Enmascaramiento dinámico de datos](https://docs.microsoft.com/en-us/sql/relational-databases/security/dynamic-data-masking) para ofuscar columnas confidenciales en uso.
* [Always Encrypted](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine) para cifrar columnas confidenciales en reposo.

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Next Steps]: #subheading-3

<!--Image references-->
[1]: ./media/sql-data-discovery-and-classification/1_data_classification_explorer_menu.png
[2]: ./media/sql-data-discovery-and-classification/2_recommendations_notification_box.png
[3]: ./media/sql-data-discovery-and-classification/3_recommendations_panel.png
[4]: ./media/sql-data-discovery-and-classification/4_recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5_accept_recommendations_button.png
[6]: ./media/sql-data-discovery-and-classification/6_add_classification_button.png
[7]: ./media/sql-data-discovery-and-classification/7_manual_classification.png
[8]: ./media/sql-data-discovery-and-classification/8_save.png
[9]: ./media/sql-data-discovery-and-classification/9_view_report.png
[10]: ./media/sql-data-discovery-and-classification/10_report.png
