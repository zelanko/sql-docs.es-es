---
title: Realización de una evaluación de migración del servicio de integración de SQL Server (Data Migration Assistant) | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para evaluar un servicio de integración de SQL Server local antes de migrar a Azure SQL Database o Azure SQL Database instancia administrada
ms.custom: ''
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
ms.openlocfilehash: 14e53b3820e784916484cbe6a15ba82cd2ed5c8e
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70001377"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Realización de una evaluación de migración del servicio de integración de SQL Server con Data Migration Assistant

Las siguientes instrucciones paso a paso le ayudarán a realizar la primera evaluación de la migración de paquetes de SQL Server Integration Service (SSIS) a Azure SQL Database o Azure SQL Database instancia administrada, con Data Migration Assistant.

## <a name="create-an-assessment"></a>Creación de una evaluación

1. Seleccione el icono de **nuevo** (+) y, a continuación, seleccione el tipo de proyecto de **evaluación** como **servicio de integración**.

1. Establezca el tipo de servidor de origen y de destino.

    Seleccione el origen como **SQL Server**y establezca el tipo de servidor de destino como **Azure SQL Database** o **Azure SQL Database instancia administrada**.

1. Haga clic en **Create**(Crear).

    ![crear evaluación](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="add-sources-to-assess"></a>Agregar orígenes para evaluar

1. Siga la opción predeterminada y haga clic en **siguiente** para **seleccionar orígenes**.

1. Escriba el nombre de la instancia de SQL Server, elija el tipo de autenticación, establezca las propiedades de conexión correctas.
1. Escriba una ruta de acceso a la carpeta que contenga paquetes SSIS
1. Escriba la contraseña de cifrado del paquetesi procede y, a continuación, conéctese.
1. Seleccione el sistema de archivos que desea evaluar y, a continuación, seleccione **Agregar**.
  ![Agregar origen](media/dma-assess-ssis/dma-assess-ssis-addsource.png)
1. Seleccione **Agregar orígenes** para abrir el menú contextual de conexión si necesita evaluar varias carpetas.
1. Haga clic en **iniciar evaluación**.
  ![Iniciar evaluación](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Vista de resultados

La categoría de problemas de compatibilidad proporciona características parcialmente compatibles o no compatibles que bloquean la migración de paquetes de SSIS locales a Azure-SSIS Integration Runtime. A continuación, se proporcionan recomendaciones para ayudarle a solucionar esos problemas.

![Vista de resultados](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Pasos siguientes

- [Migración de paquetes de SQL Server Integration Services a una instancia administrada de Azure SQL Database](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Volver a implementar paquetes de SQL Server Integration Services en Azure SQL Database](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages)
