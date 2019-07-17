---
title: Bases de datos de migración de Oracle a SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e1021643d503e1ca77f120b81046b3773f8ff458
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259101"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migración de bases de datos de Oracle a SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para Oracle es un entorno integral que le ayuda a migrar rápidamente bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB o Azure SQL Data Warehouse. Mediante el uso de SSMA para Oracle, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB o Azure SQL Data Warehouse, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB o datos de SQL Azure Almacén. Tenga en cuenta que no puede migrar esquemas SYS y del sistema Oracle.
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar correctamente los objetos y datos de bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Azure SQL DB o Azure SQL Data Warehouse, siga este procedimiento:
  
1.  [Cree un nuevo proyecto SSMA](working-with-ssma-projects-oracletosql.md).  
  
    Después de crear el proyecto, puede establecer las opciones de la asignación de tipos, migración y conversión del proyecto. Para obtener información acerca de la configuración del proyecto, vea [definir opciones de proyecto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Para obtener información sobre cómo personalizar las asignaciones de tipos de datos, vea [asignación de Oracle y SQL Server Data Types &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Conectar con el servidor de base de datos de Oracle](connecting-to-oracle-database-oracletosql.md).  
  
3.  [Conectarse a una instancia de SQL Server](connecting-to-sql-server-oracletosql.md).  
  
4.  [Asignar los esquemas de base de datos de Oracle a esquemas de base de datos de SQL Server](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
5.  Si lo desea, [crear informes de evaluación](assessing-oracle-schemas-for-conversion-oracletosql.md) para evaluar los objetos de base de datos para la conversión y estimar el tiempo de conversión.  
  
6.  [Convertir esquemas de base de datos de Oracle en los esquemas de SQL Server](converting-oracle-schemas-oracletosql.md).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
    Puede hacerlo en una de las maneras siguientes:  
  
    -   Guardar un script y ejecutarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Sincronizar los objetos de base de datos.  
  
8.  [Migrar datos a SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Introducción a SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
