---
title: Método updateObject (int, java.lang.Object) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4993dfe1-2232-4b3c-b931-dfdb35dd225a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 99a6b4c7ba565b9a77400f3ccb4e887367030a7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778210"
---
# <a name="updateobject-method-int-javalangobject"></a>Método updateObject (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor **Object** según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateObject(int index,  
                         java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Valor **int** que indica el índice de la columna.  
  
 *obj*  
  
 Valor **Object**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método updateObject especificado por el método updateObject en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateObject &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
