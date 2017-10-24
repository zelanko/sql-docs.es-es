---
title: HOST_ID (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HOST_ID
- HOST_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], workstations
- HOST_ID function
- workstation IDs [SQL Server]
- identification numbers [SQL Server], workstations
ms.assetid: 36ba56d4-20d7-4cd1-aa2a-e40a6c0a4e39
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0cf562d5e9eb868494245ba561e77aa7546d83ad
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="hostid-transact-sql"></a>HOST_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de identificación de la estación de trabajo. El número de identificación de la estación de trabajo es el identificador de proceso (PID) de la aplicación en el equipo cliente que se está conectando a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HOST_ID ()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **Char (10)**  
  
## <a name="remarks"></a>Comentarios  
 Cuando el parámetro de una función del sistema es opcional, se asumen la base de datos, el equipo host, el usuario del servidor o el usuario de la base de datos actuales. Las funciones integradas siempre deben ir seguidas de paréntesis.  
  
 Funciones de sistema se pueden usar en la lista de selección en la cláusula WHERE, y en cualquier lugar en que se permita una expresión.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una tabla que utiliza `HOST_ID()` en una definición de `DEFAULT` para registrar el identificador de terminal de los equipos que insertan filas en una tabla que registra pedidos.  
  
```  
CREATE TABLE Orders  
   (OrderID     int       PRIMARY KEY,  
    CustomerID  nchar(5)  REFERENCES Customers(CustomerID),  
    TerminalID  char(8)   NOT NULL DEFAULT HOST_ID(),  
    OrderDate   datetime  NOT NULL,  
    ShipDate    datetime  NULL,  
    ShipperID   int       NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

