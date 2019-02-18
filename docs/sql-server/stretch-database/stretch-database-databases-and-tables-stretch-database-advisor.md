---
title: Identificación de bases de datos y tablas para Stretch Database | Microsoft Docs
ms.date: 10/30/2017
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cc6869720018e6787c915fd56e5810b319c651de
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240749"
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>Identificar bases de datos y tablas para Stretch Database con Data Migration Assistant
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Para identificar bases de datos y tablas que sean aptas para Stretch Database, además de posibles problemas de bloqueo, descargue y ejecute Microsoft Data Migration Assistant.
  
## <a name="get-data-migration-assistant"></a>Obtener Data Migration Assistant
 Descargue e instale Data Migration Assistant desde [aquí](https://www.microsoft.com/download/details.aspx?id=53595). Esta herramienta no está incluida en los medios de instalación de SQL Server.  
  
## <a name="run-data-migration-assistant"></a>Ejecutar Data Migration Assistant  
  
1.  Ejecute Microsoft Data Migration Assistant.  

2.  Cree un nuevo proyecto de tipo **Evaluación** y asígnele un nombre.

3.  Seleccione **SQL Server** como **Source server type** (Tipo de servidor de origen) y **Target server type** (Tipo de servidor de destino).

4.  Seleccione **Crear**. 

5. En la página **Opciones** (paso 1), seleccione **New features recommendation** (Nueva recomendación de características). También puede desactivar **Problemas de compatibilidad**.

6.  En la página **Seleccionar orígenes** (paso 2), conéctese a un servidor, seleccione una base de datos y luego **Agregar**.

7.  Seleccione **Start Assessment** (Iniciar evaluación).

## <a name="review-the-results"></a>Consultar los resultados  
  
1.  Cuando termine el análisis, en la página **Revisar resultados** (paso 3), seleccione la opción **Recomendaciones de características** y luego la pestaña **Almacenamiento**.

2.  Revise las recomendaciones relacionadas con Stretch Database. Cada recomendación indica las tablas para las que puede ser adecuado Stretch Database, además de los posibles problemas de bloqueo.

## <a name="historical-note"></a>Nota histórica
Stretch Database Advisor antes era un componente de SQL Server 2016 Upgrade Advisor. Entonces había que seleccionar y ejecutar Stretch Database Advisor como una acción independiente.

Con el lanzamiento de Data Migration Assistant, que reemplaza a Upgrade Advisor y lo amplía, la funcionalidad de Stretch Database Advisor se ha incorporado a esta nueva herramienta. No es necesario seleccionar ninguna opción para obtener recomendaciones relacionadas con Stretch Database. Cuando se ejecuta una evaluación en Data Migration Assistant, los resultados relacionados con Stretch Database aparecen en la pestaña **Almacenamiento** de **Recomendaciones de características**.
  
## <a name="next-step"></a>Paso siguiente  
 Habilitar Stretch Database  
  
-   Para habilitar Stretch Database en una **base de datos**, vea [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Para habilitar Stretch Database en otra **tabla**, si Stretch ya está habilitado en la base de datos, vea [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Consulte también  
 [Limitaciones del área expuesta y problemas de bloqueo de Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table (Habilitar Stretch Database para una tabla)](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
