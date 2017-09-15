---
title: "Método setNString (SQLServerCallableStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6494300b-7fc0-4076-8311-22d35a96cdc6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7748fe8a19028542d76cda580f6bbb7c24f3a7a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setnstring-method-sqlservercallablestatement"></a>Método setNString (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto de cadena especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNString(java.lang.String parameterName, java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 A **cadena** que indica el nombre del parámetro.  
  
 *value*  
  
 Un objeto de cadena.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método se debería utilizar para **NCHAR**, **NVARCHAR**, **NTEXT**, y **XML** tipos de datos.  
  
 Este método setNString especificado por el método setNString en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
