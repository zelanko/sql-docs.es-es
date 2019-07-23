---
title: Constructor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72ae0e8ed3c65a795723326d7ca49e2f5a909f18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971144"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>Constructor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la clase [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) cuando se proporciona un **objeto**, un objeto de **cadena** , un objeto de **cadena** , un **entero**y un **valor booleano**.

## <a name="syntax"></a>Sintaxis  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parámetros  
 *obj*  
  
 Búfer de e/s que generó la excepción.

 *errText*  
  
 Cadena que contiene el texto del error.
  
 *sqlState*  
  
 Objeto de enumeración que contiene el estado de SQL.
 
 *errNum*  
  
 Un valor int que contiene el código de error para la excepción.
 
 *bStack*  
  
 Un valor booleano que indica si se debe generar el seguimiento de la pila.
  
## <a name="see-also"></a>Consulte también  
 [Constructores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Miembros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Clase SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
