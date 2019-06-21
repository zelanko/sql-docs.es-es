---
title: Método updateNull (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateNull (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b22336a1-fe53-4e00-a5ff-ede8d3f2b9f9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3e1b4b391cf0c2106a705e272d891158c8ab5e3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798819"
---
# <a name="updatenull-method-int"></a>Método updateNull (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor NULL según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNull(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método updateNull lo especifica el método updateNull en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateNull &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
