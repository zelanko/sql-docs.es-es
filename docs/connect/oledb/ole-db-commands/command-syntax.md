---
title: Sintaxis de comandos | Microsoft Docs
description: Sintaxis de comandos y procedimientos almacenados
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 15d6d221c9e3435a3ba4c3f58c7d6b6e55314f29
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68016121"
---
# <a name="command-syntax"></a>Sintaxis de comandos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server reconoce la sintaxis de comando especificada por la macro DBGUID_SQL. Para OLE DB Driver for SQL Server, el especificador indica que una amalgama de ODBC SQL, ISO y [!INCLUDE[tsql](../../../includes/tsql-md.md)] es sintaxis válida. Por ejemplo, la siguiente instrucción SQL utiliza una secuencia de escape de ODBC SQL para especificar la función de cadena LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE devuelve una cadena de caracteres, convirtiendo todos los caracteres en mayúscula en sus equivalentes en minúscula. La función de cadena ISO LOWER realiza la misma operación, de modo que la instrucción SQL siguiente es un equivalente ISO de la instrucción ODBC presentada anteriormente:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 El controlador OLE DB para SQL Server procesa correctamente cualquiera de los formatos de la instrucción cuando se especifica como texto para un comando.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 Al ejecutar un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante un comando del controlador OLE DB para SQL Server, use la secuencia de escape de ODBC CALL en el texto del comando. Después, el controlador OLE DB para SQL Server usa el mecanismo de la llamada a procedimiento remoto de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para optimizar el procesamiento del comando. Por ejemplo, la instrucción SQL de ODBC siguiente es el texto de comando preferido sobre la forma [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
