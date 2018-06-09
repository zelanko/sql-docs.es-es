---
title: 'Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure | Documentos de Microsoft'
ms.prod: sql
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
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1914549671a4a9ccd78ce859f59f55e5a9f9a3e4
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776741"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure (MySQLToSql)
SQL Server Migration Assistant (SSMA) para MySQL es un entorno completo que le ayuda a migrar rápidamente las bases de datos de MySQL a SQL Server o SQL Azure. Mediante el uso de SSMA para MySQL, puede revisar los datos y objetos de base de datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a SQL Server o SQL Azure y, a continuación, migrar datos a SQL Server o SQL Azure.  
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar satisfactoriamente objetos y datos de bases de datos de MySQL a SQL Server o SQL Azure, siga este procedimiento:  
  
1.  [Trabajar con proyectos SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    Después de crear el proyecto, puede establecer la conversión del proyecto, migración y opciones de la asignación de tipos. Para obtener más información acerca de la configuración de proyecto, vea [establecer las opciones del proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md). Para obtener información sobre cómo personalizar las asignaciones de tipos de datos, vea [asignación MySQL y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [Conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [Conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [Asignación de las bases de datos de MySQL a esquemas SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Conectarse a la base de datos de SQL Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  Si lo desea, [evaluar bases de datos de MySQL para la conversión &#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) para evaluar los objetos de base de datos para la conversión y calcular el tiempo de conversión.  
  
7.  [Conversión de bases de datos MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [Sincronización](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
9. Puede hacerlo en una de las maneras siguientes:  
  
    -   Guardar un script y ejecutarlo en SQL Server o SQL Azure.  
  
    -   Sincronizar los objetos de base de datos.  
  
10. [Migrar datos de MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. Si es necesario, actualizar las aplicaciones de base de datos.  
  
> [!NOTE]  
> No puede migrar esquemas Information_schema y MySQL.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Introducción a SSMA para MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
