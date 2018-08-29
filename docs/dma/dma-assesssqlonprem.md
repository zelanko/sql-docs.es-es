---
title: Realizar una evaluación de migración de SQL Server (Data Migration Assistant) | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para evaluar un servidor local SQL Server antes de migrar a otro servidor SQL Server o a Azure SQL Database
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 1a8de403a529ca5b74c6391f0e3f4cef2cca26d2
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152786"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Realizar una evaluación de migración de SQL Server con Data Migration Assistant

Las siguientes instrucciones paso a paso para ayudarán a realizar la primera evaluación para migrar a un entorno local SQL Server, SQL Server que se ejecuta en una máquina virtual de Azure o Azure SQL Database, mediante el uso de Data Migration Assistant.

## <a name="create-an-assessment"></a>Crear una evaluación

1.  Seleccione el **New** (+) icono y, a continuación, seleccione el **evaluación** tipo de proyecto.

2.  Establezca el tipo de servidor de origen y destino.

    Si va a actualizar la instancia de SQL Server local a una instancia de SQL Server modernas de forma local o a SQL Server hospedado en una máquina virtual de Azure, establezca el tipo de servidor de origen y destino **SQL Server**. Si va a migrar a Azure SQL Database, en su lugar, establezca el tipo de servidor de destino **Azure SQL Database**.

3.  Haga clic en **Crear**.

    ![Crear una evaluación](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>Elegir opciones de evaluación

1. Seleccione la versión de SQL Server de destino que va a migrar a.

2. Seleccione el tipo de informe.

   Al evaluar la instancia de SQL Server de origen para migrar a un entorno local de SQL Server o a SQL Server hospedadas en los destinos de la máquina virtual de Azure, puede elegir uno o ambos de los siguientes tipos de informe de evaluación:

    -   **Problemas de compatibilidad**

    -   **Recomendación de las nuevas características**

    ![Seleccione un tipo de informe de evaluación para el destino de SQL Server](../dma/media/AssessmentTypes.png)

   Al evaluar la instancia de SQL Server de origen para migrar a Azure SQL Database, puede elegir uno o ambos de los siguientes tipos de informe de evaluación:

    -   **Comprobar la compatibilidad de base de datos**

    -   **Comprobar paridad de características**

    ![Seleccionar tipo de informe de evaluación para el destino de la base de datos SQL](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>Agregar bases de datos para evaluar

1.  Seleccione **agregar orígenes** para abrir el menú desplegable de conexión.

2.  Escriba el nombre de instancia SQL server, elija el tipo de autenticación, establezca las propiedades de conexión correcta y, a continuación, seleccione **Connect**.

3.  Seleccione las bases de datos para evaluar y, a continuación, seleccione **agregar**.

    > [!NOTE] 
    > Puede quitar varias bases de datos seleccionando mientras mantiene presionada la tecla MAYÚS o Ctrl y, a continuación, haga clic en **quitar orígenes**. También puede agregar las bases de datos de varias instancias de SQL Server mediante el **agregar orígenes** botón.

4.  Haga clic en **siguiente** para iniciar la evaluación.

    ![Agregar orígenes e iniciar evaluación](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>Ver los resultados

La duración de la evaluación depende el número de bases de datos agregadas y el tamaño del esquema de cada base de datos. Los resultados se muestran para cada base de datos tan pronto como estén disponibles.

1.  Seleccione la base de datos que se ha completado la evaluación y, a continuación, cambiar entre **problemas de compatibilidad** y **recomendaciones de características** mediante el selector.

2.  Revise los problemas de compatibilidad en todos los niveles de compatibilidad admitidos por la versión de SQL Server de destino que se han seleccionado en el **opciones** página.

Puede revisar los problemas de compatibilidad mediante el análisis de objeto afectado, sus detalles y, potencialmente una solución para cada problema identificado en **cambios importantes**, **los cambios de comportamiento**, y  **Características desusadas**.

![Ver los resultados de evaluación](../dma/media/ReviewResults.png)

De forma similar, puede revisar la recomendación de característica a través de **rendimiento**, **almacenamiento**, y **seguridad** áreas.

Recomendación de característica abarcan una gran variedad de características como OLTP en memoria y almacén de columnas, Stretch Database, Always Encrypted, enmascaramiento dinámico de datos y cifrado de datos transparente.

![Recomendaciones de características de vista](../dma/media/FeatureRecommendations.png)

Para Azure SQL Database, las evaluaciones proporcionan los problemas de bloqueo de migración y problemas de paridad de características. Revise los resultados para ambas categorías seleccionando las opciones específicas.

- El **paridad de características de SQL Server** categoría proporciona un conjunto completo de recomendaciones, alternativas disponibles en Azure y pasos de mitigación. Le ayuda a planear este trabajo en los proyectos de migración.

  ![Ver la información de paridad de características de SQL Server](../dma/media/SQLFeatureParity.png)

- El **problemas de compatibilidad** categoría proporciona características no admitidas o parcialmente compatibles que bloquean migrar bases de datos de SQL Server local a Azure SQL Database. A continuación, proporciona recomendaciones para ayudarle a resolver esos problemas.

  ![Problemas de compatibilidad de vista](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>Exportar resultados

Después de todas las bases de datos de la evaluación, seleccione **Exportar informe** para exportar los resultados a un archivo JSON o un archivo CSV. A continuación, puede analizar los datos con total libertad.

Puede ejecutar varias evaluaciones simultáneamente y ver el estado de las evaluaciones abriendo el **todas las evaluaciones** página.
