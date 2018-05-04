---
title: Bases de datos de DB2 migrar a SQL Server (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a9fb6df72470fb6b23ddee64b196da24cd7c128c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrar bases de datos de DB2 a SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) para DB2 es un entorno integral que le ayuda a migrar rápidamente bases de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Mediante el uso de SSMA para DB2, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Tenga en cuenta que no puede migrar esquemas SYS y sistema DB2.  
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar correctamente los objetos y datos de bases de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, siga este procedimiento:  
  
1.  [Nuevo proyecto SSMA](http://msdn.microsoft.com/en-us/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Después de crear el proyecto, puede establecer la conversión del proyecto, migración y opciones de la asignación de tipos. Para obtener información acerca de la configuración de proyecto, vea [configuración del proyecto &#40;conversión&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) y secciones relacionadas. Para obtener información sobre cómo personalizar las asignaciones de tipos de datos, vea [asignación DB2 y tipos de datos de SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conectarse a la base de datos de DB2](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Conectarse a SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Asignar los esquemas de DB2 a esquemas de SQL Server](http://msdn.microsoft.com/en-us/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Si lo desea, [informes de evaluación](http://msdn.microsoft.com/en-us/9e13eba0-e3cf-4205-974f-c00f982061de) para evaluar los objetos de base de datos para la conversión y calcular el tiempo de conversión.  
  
6.  [Convertir esquemas de DB2](http://msdn.microsoft.com/en-us/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Puede hacerlo en una de las maneras siguientes:  
  
    -   Guardar un script y ejecútelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Sincronizar los objetos de base de datos.  
  
8.  [Migrar datos de DB2 en SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Si es necesario, actualizar las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introducción a SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
