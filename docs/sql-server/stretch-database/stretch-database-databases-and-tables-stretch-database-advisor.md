---
title: 'Bases de datos y tablas de Stretch Database: Asesor de Stretch Database | Microsoft Docs'
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 59608301d353d99eb710a956389fd9f8d8948dfe
ms.contentlocale: es-es
ms.lasthandoff: 07/29/2017

---
# <a name="stretch-database-databases-and-tables---stretch-database-advisor"></a>Stretch Database databases and tables - Stretch Database Advisor (Bases de datos y tablas de Stretch Database: Asesor de Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para saber qué bases de datos y tablas son aptas para Stretch Database, descargue el Asesor de actualizaciones de SQL Server 2016 y ejecute el Asesor de Stretch Database. El Asesor de Stretch Database también detecta problemas de bloqueo.  
  
## <a name="download-and-install-upgrade-advisor"></a>Descargar e instalar el Asesor de actualizaciones  
 Descargue e instale el Asesor de actualizaciones desde [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=53595). Esta herramienta no se incluye en los medios de instalación de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .  
  
## <a name="run-the-stretch-database-advisor"></a>Ejecutar el Asesor de Stretch Database  
  
1.  Ejecute el Asesor de actualizaciones.  
  
2.  Seleccione **Escenarios**y luego seleccione **EJECUTAR ASESOR DE STRETCH DATABASE**.  
  
3.  En la hoja **Ejecutar Asesor de Stretch Database** , haga clic en **SELECCIONAR LAS BASES DE DATOS PARA ANALIZAR**.  
  
4.  En la hoja **Seleccionar bases de datos** , escriba o seleccione el nombre de servidor y la información de autenticación. Haga clic en **Conectar**.

5.  Aparece una lista de bases de datos en el servidor seleccionado. Seleccione las bases de datos que quiere analizar. Haga clic en **Seleccionar**.  
  
6.  En la hoja **Ejecutar Asesor de Stretch Database** , haga clic en **Ejecutar**.  Se ejecuta el análisis.  
  
## <a name="review-the-results"></a>Consultar los resultados  
  
1.  Cuando finalice el análisis, en la hoja **Analyzed databases (Bases de datos analizadas)** , seleccione una de las bases de datos que ha analizado para mostrar la hoja **Resultados del análisis** .  
  
     La hoja **Resultados del análisis** enumera las tablas recomendadas en la base de datos seleccionada que coinciden con los criterios de recomendación predeterminados. 
  
2.  En la lista de tablas de la hoja **Resultados del análisis** , seleccione una de las tablas recomendadas para mostrar la hoja **Resultados de tabla** .  
  
     Si existen problemas de bloqueo, la hoja **Resultados de tabla** enumera los problemas de bloqueo de la tabla seleccionada. Para obtener información sobre los problemas de bloqueo que ha detectado el Asesor de Stretch Database, vea [Limitaciones del área expuesta y problemas de bloqueo de Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).  
  
3.  En la lista de problemas de bloqueo de la hoja **Resultados de tabla** , seleccione uno de los problemas para mostrar más información sobre el problema seleccionado y proponer pasos de mitigación. Implemente los pasos de mitigación sugeridos si quiere configurar la tabla seleccionada para Stretch Database.  
  
## <a name="next-step"></a>Paso siguiente  
 Habilitar Stretch Database  
  
-   Para habilitar Stretch Database en una **base de datos**, vea [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Para habilitar Stretch Database en otra **tabla**, si Stretch ya está habilitado en la base de datos, vea [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Vea también  
 [Limitaciones del área expuesta y problemas de bloqueo de Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table (Habilitar Stretch Database para una tabla)](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  

