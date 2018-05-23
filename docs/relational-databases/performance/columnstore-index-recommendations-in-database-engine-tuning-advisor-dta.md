---
title: Recomendaciones de índice de almacén de columnas en el Asistente para la optimización de motor de base de datos (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4796adbefa6e4e2f89cee36c9ddee2fe05db00d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>Recomendaciones de índice de almacén de columnas en el Asistente para la optimización de motor de base de datos (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

 
  Las cargas de trabajo de análisis y el almacenamiento de datos pueden beneficiarse en gran medida de los [índices de almacén de columnas](../../t-sql/statements/create-columnstore-index-transact-sql.md), así como los índices de almacén de filas tradicionales. La elección de los índices de almacén de columnas y de filas que se generará es dependiente de la carga de trabajo de la aplicación. En SQL Server 2016, el [Asistente para la optimización de motor de base de datos (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) puede analizar la carga de trabajo y recomienda una combinación adecuada de índices de almacén y de columnas para crear la base de datos. 
  
 Esta característica está disponible con SQL Server Management Studio versión **16.4** o superior. 
  
## <a name="how-to-enable-columnstore-index-recommendations-in-database-engine-tuning-advisor-gui"></a>Procedimiento para habilitar recomendaciones de índice de almacén de columnas en la GUI del Asistente para la optimización de motor de base de datos

  
  1. Inicie el Asistente para la optimización de motor de base de datos y abra una nueva sesión de optimización.
  
  2. Seleccione las bases de datos y la carga de trabajo para la optimización en el panel **General**.
  
  3. En el panel de Opciones de optimización, marque la casilla de verificación **Recomendar índices de almacén de columnas** (consulte la figura siguiente).
  ![Opción de optimización de índices de almacén de columnas de DTA](../../relational-databases/performance/media/dta-columnstore-indexes-tuning-option.gif)
 
  4. Seleccione otras opciones de optimización y haga clic en el botón **Iniciar análisis**.
  
  5. Una vez finalizada la optimización, vea todas las recomendaciones, incluidos los índices de almacén de columnas en el panel **Recomendaciones** (consulte la figura siguiente).      
  ![Recomendación de índices de almacén de columnas de DTA](../../relational-databases/performance/media/dta-columnstore-index-recommendation.gif)
  
  6. Haga clic en el hipervínculo **Definición** para ver la instrucción de lenguaje de definición de datos (DDL) de SQL que puede crear el índice recomendado. De forma predeterminada, DTA utiliza el sufijo **col** el nombre de los índices de almacén de columnas para que sea más fácil identificar los índices de almacén de columnas (consulte la figura siguiente).
  ![Definición de índices de almacén de columnas de DTA](../../relational-databases/performance/media/dta-columnstore-index-definition.gif) 
  
  
  ## <a name="how-to-enable-columnstore-index-recommendations-in-dtaexe-utility"></a>Procedimiento para habilitar las recomendaciones de índices de almacén de columnas en la utilidad dta.exe

Para habilitar las recomendaciones del almacén de columnas cuando se usa la utilidad de línea de comandos dta.exe, use el parámetro de línea de comandos **fc-**.

Para obtener información sobre la utilidad de línea de comandos dta.exe, vea [dta (utilidad)](../../tools/dta/dta-utility.md).

## <a name="see-also"></a>Ver también
[Guía de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[Tutorial: Asistente para la optimización de motor de base de datos](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)



  

