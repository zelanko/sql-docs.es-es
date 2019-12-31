---
title: Cree una evaluación de migración de SSIS con el Data Migration Assistant
description: Aprenda a usar Data Migration Assistant para evaluar un servicio de integración SQL Server (SSIS) local antes de migrar a Azure SQL Database o Azure SQL Database instancia administrada
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.custom: seo-lt-2019
ms.openlocfilehash: 1652d5eec9d6419e7b39f96a8b854eef8651bf26
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687158"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Realización de una evaluación de migración del servicio de integración de SQL Server con Data Migration Assistant

## <a name="prerequisites"></a>Requisitos previos

Para evaluar los paquetes de SQL Server Integration Service (SSIS), los componentes siguientes deben instalarse con Data Migration Assistant:

- SQL Server servicio de integración con la misma versión que los paquetes SSIS que se van a evaluar.
- Feature Pack de Azure u otros componentes de terceros si los paquetes SSIS que se van a evaluar tienen estos componentes.  

DMA debe ejecutarse con acceso de administrador para evaluar **los** paquetes SSIS en el almacén de paquetes.

## <a name="performance-assessments"></a>Evaluaciones de rendimiento

Las siguientes instrucciones paso a paso le ayudarán a realizar la primera evaluación de la migración de paquetes de SQL Server Integration Service (SSIS) a Azure SQL Database o Azure SQL Database instancia administrada, con Data Migration Assistant.

## <a name="create-an-assessment"></a>Crear una evaluación

1. Seleccione el icono de **nuevo** (+) y, a continuación, seleccione el tipo de proyecto de **evaluación** como **servicio de integración**.

1. Establezca el tipo de servidor de origen y de destino.

    Seleccione el origen como **SQL Server**y establezca el tipo de servidor de destino como **Azure SQL Database** o **Azure SQL Database instancia administrada**.

1. Haga clic en **Crear**.

    ![crear evaluación](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="connect-to-a-server"></a>Conexión a un servidor

1. Siga la opción predeterminada y haga clic en **siguiente** para **seleccionar orígenes**.
1. Escriba el nombre de la instancia de SQL Server, elija el tipo de autenticación, establezca las propiedades de conexión correctas.
1. Opta Escriba una ruta de acceso a la carpeta que contenga paquetes SSIS.
1. Opta Escriba la contraseña de cifrado del paquete si procede.
1. Haga clic en **conectar** con el servidor SQL Server de origen.
  ![Agregar origen](media/dma-assess-ssis/dma-assess-ssis-addsource.png)

## <a name="add-sources-to-assess"></a>Agregar orígenes para evaluar

1. Seleccione los tipos de almacenamiento de paquetes SSIS que desea evaluar y, a continuación, seleccione **Agregar**.
![Agregar origen](media/dma-assess-ssis/dma-assess-ssis-addsource-type.png)
1. Seleccione **Agregar orígenes** para abrir el menú contextual de conexión si necesita evaluar varias carpetas.
1. Haga clic en **Iniciar evaluación**.
  ![Iniciar evaluación](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Visualización de los resultados

La categoría de problemas de compatibilidad proporciona características parcialmente compatibles o no compatibles que bloquean la migración de paquetes de SSIS locales a Azure-SSIS Integration Runtime. A continuación, se proporcionan recomendaciones para ayudarle a solucionar esos problemas.

![Visualización de los resultados](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Pasos siguientes

- [Información general sobre la migración de cargas de trabajo de SSIS locales a SSIS en ADF](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [Migración de paquetes de SQL Server Integration Services a una instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Reimplementación de paquetes de SQL Server Integration Services a Azure SQL Database](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
