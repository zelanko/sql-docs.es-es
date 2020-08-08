---
title: Migración de bases de datos de Sybase ASE a SQL Server Azure SQL Database | Microsoft Docs
description: Utilice este proceso recomendado para migrar bases de datos empresariales de SAP Adaptive Server a SQL Server o Azure SQL Database mediante SQL Server Migration Assistant (SSMA).
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e0a938d615b15dc7b280a6c6b9337a546e0059bf
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934701"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migración de bases de datos de SAP ASE a SQL Server-Azure SQL Database (SybaseToSQL)
SQL Server Migration Assistant (SSMA) para SAP Adaptive Server Enterprise (ASE) es un entorno completo que le ayuda a migrar rápidamente las bases de datos de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Con SSMA para SAP ASE, puede revisar los datos y los objetos de base de datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.  
  
## <a name="recommended-migration-process"></a>Proceso de migración recomendado  
Para migrar correctamente objetos y datos de bases de datos de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, utilice el siguiente proceso:  
  
1.  [Cree un nuevo proyecto de SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Después de crear el proyecto, puede establecer las opciones de conversión de proyectos, migración y asignación de tipos. Para obtener información sobre la configuración del proyecto, vea [establecer opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obtener información acerca de cómo personalizar las asignaciones de tipos de datos, consulte [asignación de tipos de datos de Sybase ase y SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conéctese al servidor de base de datos de SAP ase](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Conéctese a una instancia SQL Server](connecting-to-sql-server-sybasetosql.md) o [Conéctese a una instancia de Azure SQL Database](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Asignación de esquemas de base de datos de SAP ase a esquemas de base de datos de SQL Server/Azure SQL Database](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Opcionalmente, [cree informes de evaluación](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) para evaluar los objetos de base de datos para la conversión y calcular el tiempo de conversión.  
  
6.  [Convierta los esquemas de base de datos de SAP ase en esquemas de SQL Server/Azure SQL Database](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Cargue los objetos de base de datos convertidos en SQL Server/Azure SQL Database](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Guarde un script y ejecútelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, o bien sincronice los objetos de base de datos.  
  
8.  [Migre los datos a SQL Server/Azure SQL Database](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Consulte también  
[Instalación de SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introducción con SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
