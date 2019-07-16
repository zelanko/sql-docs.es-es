---
title: 'Migrar bases de datos MySQL a SQL Server: base de datos SQL de Azure | Microsoft Docs'
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 33dd7faf67e82f1259ac87a0ef8e0eb5fdf2927d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908798"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>Migrar bases de datos de MySQL a SQL Server: Azure SQL DB (MySQLToSql)
SQL Server Migration Assistant (SSMA) para MySQL es un entorno completo que le permite migrar rápidamente bases de datos MySQL a SQL Server o SQL Azure. Mediante el uso de SSMA para MySQL, puede revisar los datos y objetos de base de datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a SQL Server o SQL Azure y, a continuación, migrar datos a SQL Server o SQL Azure.  
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar satisfactoriamente objetos y datos de bases de datos MySQL a SQL Server o SQL Azure, use el siguiente proceso:  
  
1.  [Proyectos de SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    Después de crear el proyecto, puede establecer las opciones de la asignación de tipos, migración y conversión del proyecto. Para obtener más información acerca de la configuración del proyecto, vea [definir opciones de proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md). Para obtener información sobre cómo personalizar las asignaciones de tipos de datos, vea [asignación MySQL y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [Conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [Conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [Asignación de bases de datos MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Conexión a Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  Si lo desea, [evaluar bases de datos de MySQL para la conversión &#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) para evaluar los objetos de base de datos para la conversión y estimar el tiempo de conversión.  
  
7.  [Conversión de bases de datos MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [Sincronización](loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
9. Puede hacerlo en una de las maneras siguientes:  
  
    -   Guardar un script y ejecutarlo en SQL Server o SQL Azure.  
  
    -   Sincronizar los objetos de base de datos.  
  
10. [Migrar datos de MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. Si es necesario, actualice las aplicaciones de base de datos.  
  
> [!NOTE]  
> No puede migrar esquemas Information_schema y MySQL.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Introducción a SSMA para MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
