---
title: Realizar una evaluación de la migración de SQL Server (Asistente de migración de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 42cd32f57547f811fba379caa3bef5678dc2b50b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="perform-a-sql-server-migration-assessment"></a>Realizar una evaluación de la migración de SQL Server
Las siguientes instrucciones paso a paso ayudarán a realizar la primera evaluación para migrar a local SQL Server, SQL Server que se ejecuta en una máquina virtual de Azure o base de datos de SQL Azure, mediante el Asistente de migración de datos.

## <a name="create-an-assessment"></a>Crear una evaluación

1.  Seleccione el **New** (+) icono y, a continuación, seleccione la **evaluación** tipo de proyecto.

2.  Establecer el tipo de servidor de origen y de destino.

    Si va a actualizar la instancia de SQL Server local a una instancia de SQL Server local moderna o a SQL Server hospedado en una máquina virtual de Azure, establezca el tipo de servidor de origen y de destino en **SQL Server**. Si va a migrar a base de datos de SQL Azure, en su lugar, Establece el tipo de servidor de destino en **base de datos de SQL Azure**.

3.  Haga clic en **Crear**.

    ![Crear una evaluación](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>Elegir opciones de evaluación

1. Seleccione la versión de SQL Server de destino que va a migrar a.

2. Seleccione el tipo de informe.

   Cuando se está evaluando la instancia de SQL Server de origen para migrar a local SQL Server o SQL Server hospedado en destinos de la máquina virtual de Azure, puede elegir uno o ambos de los siguientes tipos de informes de evaluación:

    -   **Problemas de compatibilidad**

    -   **Recomendación de nuevas características**

    ![Seleccione un tipo de informe de evaluación de destino de SQL Server](../dma/media/AssessmentTypes.png)

   Cuando se está evaluando la instancia de SQL Server de origen para migrar a base de datos de SQL Azure, puede elegir uno o ambos de los siguientes tipos de informes de evaluación:

    -   **Comprobar la compatibilidad de base de datos**

    -   **Comprobar una paridad de características**

    ![Seleccionar tipo de informe de evaluación de destino de la base de datos SQL](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>Agregar bases de datos para evaluar

1.  Seleccione **agregar orígenes** para abrir el menú desplegable de conexión.

2.  Escriba el nombre de instancia SQL server, elija el tipo de autenticación, establezca las propiedades de conexión correcta y, a continuación, seleccione **conectar**.

3.  Seleccione las bases de datos para evaluar y, a continuación, seleccione **agregar**.

    > [!NOTE] 
    > Puede quitar varias bases de datos mediante la selección de ellas mientras mantiene presionada la tecla MAYÚS o Ctrl y, a continuación, haga clic en **quitar orígenes**. También puede agregar las bases de datos de varias instancias de SQL Server mediante la **agregar orígenes** botón.

4.  Haga clic en **siguiente** para iniciar la evaluación.

    ![Agregar orígenes e iniciar la evaluación](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>Ver los resultados

La duración de la evaluación depende el número de bases de datos agregadas y el tamaño del esquema de cada base de datos. Resultados se muestran para cada base de datos en cuanto están disponibles.

1.  Seleccione la base de datos que se ha completado la evaluación y, a continuación, cambiar entre **problemas de compatibilidad** y **característica recomendaciones** utilizando el modificador.

2.  Revise los problemas de compatibilidad en todos los niveles de compatibilidad admitidos por la versión de SQL Server de destino que se han seleccionado en el **opciones** página.

Puede revisar los problemas de compatibilidad al analizar el objeto afectado y sus detalles para cada problema identificado en **cambios importantes**, **cambios de comportamiento**, y **las características en desuso** .

![Ver los resultados de evaluación](../dma/media/ReviewResults.png)

De forma similar, puede revisar la recomendación de característica a través de **rendimiento**, **almacenamiento**, y **seguridad** áreas.

Recomendaciones de característica abarcan una gran variedad de características como OLTP en memoria y almacén de columnas, Stretch Database, Always Encrypted, enmascaramiento de datos dinámicos y cifrado de datos transparente.

![Recomendaciones de la característica de vista](../dma/media/FeatureRecommendations.png)

Base de datos de SQL Azure, las evaluaciones proporcionan los problemas de bloqueo de migración y problemas de paridad de características. Revise los resultados de ambas categorías seleccionando las opciones específicas.

- El **paridad de características de SQL Server** categoría proporciona un conjunto completo de recomendaciones, alternativas disponibles en Azure y pasos. Le ayuda a planear este trabajo en los proyectos de migración.

  ![Ver la información de paridad de características de SQL Server](../dma/media/SQLFeatureParity.png)

- El **problemas de compatibilidad** categoría proporciona características no admitidas o admitidas parcialmente que bloquean migrar bases de datos de SQL Server local a bases de datos de SQL Azure. A continuación, proporciona recomendaciones para ayudarle a resolver esos problemas.

  ![Problemas de compatibilidad de vista](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>Exportar resultados

Después de todas las bases de datos de la evaluación, seleccione **Exportar informe** para exportar los resultados en un archivo JSON o en un archivo CSV. A continuación, puede analizar los datos en su propia comodidad.

Puede ejecutar simultáneamente varias evaluaciones y ver el estado de las evaluaciones abriendo el **todas las evaluaciones** página.
