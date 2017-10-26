---
title: "cadena de método al objeto de lector - setNCharacterStream | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fd19fbb8-a878-4d98-a584-e4969d649844
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51250ced4a6925bba1493346f48ddc6035b20005
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setncharacterstream-method-javalangstring-javaioreader"></a>Método setNCharacterStream (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para el objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                       java.io.Reader value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 A **cadena** que indica el nombre del parámetro.  
  
 *value*  
  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setNCharacterStream especificado por el método setNCharacterStream en la interfaz java.sql.CallableStatement.  
  
 Este método se debería utilizar para **NCHAR**, **NVARCHAR**, **NTEXT**, y **XML** tipos de datos.  
  
## <a name="see-also"></a>Vea también  
 [Método setNCharacterStream &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

