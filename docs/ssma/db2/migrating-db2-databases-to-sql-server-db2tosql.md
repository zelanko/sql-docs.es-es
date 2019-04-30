---
title: Las bases de datos DB2 migrar a SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8ee6e9cca2e16a180f869df7bcec07bb7b09e390
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63071151"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrar bases de datos de DB2 a SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para DB2 es un entorno integral que le ayuda a migrar rápidamente bases de datos DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Mediante el uso de SSMA para DB2, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Tenga en cuenta que no puede migrar esquemas SYS y sistema DB2.  
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar correctamente los objetos y datos de bases de datos DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, utilice el siguiente proceso:  
  
1.  [Nuevo proyecto SSMA](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Después de crear el proyecto, puede establecer las opciones de la asignación de tipos, migración y conversión del proyecto. Para obtener información acerca de la configuración del proyecto, vea [configuración del proyecto &#40;conversión&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) y secciones relacionadas. Para obtener información sobre cómo personalizar las asignaciones de tipos de datos, vea [asignación DB2 y tipos de datos de SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conectarse a la base de datos DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Conectarse a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Asignar los esquemas de DB2 a esquemas de SQL Server](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Si lo desea, [informes de evaluación](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) para evaluar los objetos de base de datos para la conversión y estimar el tiempo de conversión.  
  
6.  [Convertir esquemas de DB2](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Puede hacerlo en una de las maneras siguientes:  
  
    -   Guardar un script y ejecutarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Sincronizar los objetos de base de datos.  
  
8.  [Migración de datos de DB2 en SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introducción a SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
