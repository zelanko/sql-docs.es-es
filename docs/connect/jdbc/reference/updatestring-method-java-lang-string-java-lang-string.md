---
title: Método updateString (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateString (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3a9236bb-a307-45a8-b7d2-c4cbd9b3cb35
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 19a54fbfe280a4a5a16b57befee87a8f46de6a6b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67998239"
---
# <a name="updatestring-method-javalangstring-javalangstring"></a>Método updateString (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor **string** según el nombre de columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateString(java.lang.String columnName,  
                         java.lang.String x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Valor **String** que contiene el nombre de columna.  
  
 *x*  
  
 Un objeto **String**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateString especifica este método updateString en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [updateString (método) &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
