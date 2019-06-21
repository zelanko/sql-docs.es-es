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
manager: jroth
ms.openlocfilehash: 868e14c72fbb7c32d394df2fbbdf5cd3a7c36738
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66766991"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>Constructor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) clase cuando se especifica un **objeto**, un **cadena** objeto, un **cadena** (objeto), un **int**y un **booleano**.

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
  
 El búfer de E/S que generó la excepción.

 *errText*  
  
 Una cadena que contiene el texto del error.
  
 *sqlState*  
  
 Un objeto de enumeración que contiene el estado SQL.
 
 *errNum*  
  
 Un valor int que contienen el código de error para la excepción.
 
 *bStack*  
  
 Un valor booleano que indica si se debe generar el seguimiento de pila.
  
## <a name="see-also"></a>Consulte también  
 [Constructores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Miembros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Clase SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
