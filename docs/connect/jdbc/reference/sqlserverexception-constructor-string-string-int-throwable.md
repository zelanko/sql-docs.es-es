---
title: SQLServerException Constructor (java.lang.String, java.lang.String, int, java.lang.Throwable) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f596056d830ae3fa3462095e5a17a112c8f641f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759263"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException Constructor (java.lang.String, java.lang.String, int, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) clase cuando se especifica un **cadena** objeto, un **cadena** objeto, un **int**y un **puede producir** objeto.

## <a name="syntax"></a>Sintaxis  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parámetros  
 *errText*  
  
 Una cadena que contiene el texto del error.
  
 *errState*  
  
 Una cadena que contiene el estado del error.
 
 *errNum*  
  
 Un entero que contiene el código de error para la excepción.
 
 *cause*  
  
 Un objeto puede producir que contiene la causa de la excepción.
  
## <a name="see-also"></a>Ver también  
 [Constructores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Miembros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Clase SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
