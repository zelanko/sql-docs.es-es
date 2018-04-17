---
title: Sintaxis del comando | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7b1f7f30dcea246be133e8eeeebba842fdaa7031
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="command-syntax"></a>Sintaxis de comandos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client reconoce la sintaxis del comando especificado por la macro DBGUID_SQL. Para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, el especificador indica que una amalgama de ODBC SQL, ISO, y [!INCLUDE[tsql](../../includes/tsql-md.md)] es una sintaxis válida. Por ejemplo, la siguiente instrucción SQL utiliza una secuencia de escape de ODBC SQL para especificar la función de cadena LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE devuelve una cadena de caracteres, convirtiendo todos los caracteres en mayúscula en sus equivalentes en minúscula. La función de cadena ISO LOWER realiza la misma operación, de modo que la instrucción SQL siguiente es un equivalente ISO de la instrucción ODBC presentada anteriormente:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client procesa cualquiera de las formas de la instrucción correctamente cuando se especifica como texto de un comando.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 Cuando se ejecuta un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacenados procedimiento mediante un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB de comandos, utilice la secuencia de escape ODBC CALL en el texto del comando. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB, a continuación, utiliza el mecanismo de llamada a procedimiento remoto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para optimizar el procesamiento de comandos. Por ejemplo, la instrucción SQL de ODBC siguiente es el texto de comando preferido sobre la forma [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
