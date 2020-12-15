---
title: Procesando resultados de procedimientos almacenados | Microsoft Docs
description: Obtenga información sobre los mecanismos SQL Server procedimientos almacenados que se usan para devolver datos a las aplicaciones. Las aplicaciones deben ser capaces de administrar todos estos tipos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1e01b61f3eb19b06b9f61653fe839818e52702d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97437546"
---
# <a name="processing-stored-procedure-results"></a>Procesar resultados de procedimientos almacenados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen cuatro mecanismos que se utilizan para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   Un parámetro de salida del cursor puede devolver un cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 Las aplicaciones deben ser capaces de administrar todos estos resultados de los procedimientos almacenados. La instrucción CALL o EXECUTE debería incluir los marcadores de parámetros para el código de retorno y los parámetros de salida. Utilice [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para enlazarlos todos como parámetros de salida y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client transferirá los valores de salida a las variables enlazadas. Los parámetros de salida y los códigos de retorno son los últimos elementos devueltos por el cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; no se devuelven a la aplicación hasta que [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) devuelve SQL_NO_DATA.  
  
 ODBC no permite enlazar parámetros de cursor [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puesto que todos los parámetros de salida se deben enlazar antes de ejecutar un procedimiento, las aplicaciones ODBC no pueden llamar a ningún procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenga un parámetro de cursor de salida.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
