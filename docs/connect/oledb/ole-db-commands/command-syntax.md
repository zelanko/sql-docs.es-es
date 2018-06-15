---
title: Sintaxis del comando | Documentos de Microsoft
description: Sintaxis de comando y los procedimientos almacenados
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a3ea215d3596842503517a9485187ba2b1368059
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665755"
---
# <a name="command-syntax"></a>Sintaxis de comandos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server reconoce la sintaxis del comando especificado por la macro DBGUID_SQL. Para el controlador OLE DB para SQL Server, el especificador indica que una amalgama de ODBC SQL, ISO, y [!INCLUDE[tsql](../../../includes/tsql-md.md)] es una sintaxis válida. Por ejemplo, la siguiente instrucción SQL utiliza una secuencia de escape de ODBC SQL para especificar la función de cadena LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE devuelve una cadena de caracteres, convirtiendo todos los caracteres en mayúscula en sus equivalentes en minúscula. La función de cadena ISO LOWER realiza la misma operación, de modo que la instrucción SQL siguiente es un equivalente ISO de la instrucción ODBC presentada anteriormente:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 El controlador OLE DB para SQL Server procesa cualquiera de las formas de la instrucción correctamente cuando se especifica como texto de un comando.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 Cuando se ejecuta un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procedimiento almacenado mediante un controlador de OLE DB para el comando de SQL Server, use la secuencia de escape ODBC CALL en el texto del comando. El controlador OLE DB para SQL Server, a continuación, utiliza el mecanismo de llamada a procedimiento remoto de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para optimizar el procesamiento de comandos. Por ejemplo, la instrucción SQL de ODBC siguiente es el texto de comando preferido sobre la forma [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
