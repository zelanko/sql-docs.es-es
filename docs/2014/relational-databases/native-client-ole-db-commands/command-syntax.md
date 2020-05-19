---
title: Sintaxis de comandos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4002a3e92bc731eaa440fc85da98b7e8b3207d5c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708023"
---
# <a name="command-syntax"></a>Sintaxis de comandos
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client reconoce la sintaxis de comandos especificada por la macro DBGUID_SQL. Para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client, el especificador indica que una amalgama de ODBC SQL, ISO y [!INCLUDE[tsql](../../includes/tsql-md.md)] es una sintaxis válida. Por ejemplo, la siguiente instrucción SQL utiliza una secuencia de escape de ODBC SQL para especificar la función de cadena LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE devuelve una cadena de caracteres, convirtiendo todos los caracteres en mayúscula en sus equivalentes en minúscula. La función de cadena ISO LOWER realiza la misma operación, de modo que la instrucción SQL siguiente es un equivalente ISO de la instrucción ODBC presentada anteriormente:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client procesa cualquier forma de la instrucción correctamente cuando se especifica como texto para un comando.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 Al ejecutar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimiento almacenado mediante un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comando de proveedor de OLE DB de Native Client, utilice la secuencia de escape ODBC Call en el texto del comando. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]A continuación, el proveedor de OLE DB de Native Client utiliza el mecanismo de llamada a procedimiento remoto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para optimizar el procesamiento de comandos. Por ejemplo, la instrucción SQL de ODBC siguiente es el texto de comando preferido sobre la forma [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Comandos](commands.md)  
  
  
