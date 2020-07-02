---
title: SQLSTATE (códigos de error ODBC) | Microsoft Docs
description: Cuando SQL Server controlador ODBC ejecuta procedimientos almacenados como procedimientos almacenados remotos, el procedimiento puede tener códigos de retorno y parámetros de salida enteros.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4efb5bae1383e64bf8b2d13c7f667183e617689d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787963"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  SQLSTATE proporciona información detallada sobre la causa de una advertencia o error. En el caso de los errores que se producen en el origen de datos detectado y devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client asigna el número de error nativo devuelto al SQLSTATE adecuado. Si un número de error nativo no tiene un código de error ODBC al que asignar, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve SQLSTATE 42000 ("error de sintaxis o infracción de acceso"). En el caso de los errores detectados por el controlador, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client genera el SQLSTATE adecuado.  
  
 Para obtener más información sobre los códigos de error de estado, vea los temas siguientes:  
  
-   [Apéndice A: Códigos de error de ADO](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Asignaciones SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
