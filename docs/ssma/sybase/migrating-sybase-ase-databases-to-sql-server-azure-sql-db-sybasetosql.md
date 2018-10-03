---
title: 'Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL de Azure | Microsoft Docs'
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 551808268b4f6eb8a0d5c16c14bcb16ba977ce61
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738183"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrar bases de datos de SAP ASE a SQL Server: Azure SQL Database (SybaseToSQL)
SQL Server Migration Assistant (SSMA) para SAP Adaptive Server Enterprise (ASE) es un entorno integral que le ayuda a migrar rápidamente bases de datos de SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Mediante el uso de SSMA para SAP ASE, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.  
  
## <a name="recommended-migration-process"></a>Proceso de migración recomendado  
Para migrar correctamente los objetos y datos de bases de datos de SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, utilice el siguiente proceso:  
  
1.  [Cree un nuevo proyecto SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Después de crear el proyecto, puede establecer las opciones de la asignación de tipos, migración y conversión del proyecto. Para obtener información acerca de la configuración del proyecto, vea [definir opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obtener información acerca de cómo personalizar las asignaciones de tipos de datos, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conectar con el servidor de base de datos de SAP ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Conectarse a una instancia de SQL Server](connecting-to-sql-server-sybasetosql.md) o [conecta a una instancia de Azure SQL Database](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Asignar los esquemas de base de datos de SAP ASE a SQL Server / esquemas de base de datos de Azure SQL Database](http://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Si lo desea, [crear informes de evaluación](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) para evaluar los objetos de base de datos para la conversión y estimar el tiempo de conversión.  
  
6.  [Convertir esquemas de base de datos de SAP ASE en SQL Server / esquemas de base de datos de SQL Azure](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server / Azure SQL Database](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Guardar un script y ejecutarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, o sincronizar los objetos de base de datos.  
  
8.  [Migrar datos a SQL Server / Azure SQL Database](http://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introducción a SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
