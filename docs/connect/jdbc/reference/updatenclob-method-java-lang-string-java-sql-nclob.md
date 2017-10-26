---
title: "Método updateNClob (java.lang.String, java.sql.NClob) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a025d124-3634-49fa-8bb5-e9b98f2d5de3
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4e5b5307bfb87e0d8b5b29c0a6a35682d18e9319
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updatenclob-method-javalangstring-javasqlnclob"></a>Método updateNClob (java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un **NClob** valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.sql.NClob x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 A **cadena** que indica la etiqueta de columna.  
  
 *x*  
  
 Un objeto NClob.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateNClob especificado por el método updateNClob en la interfaz java.sql.ResultSet.  
  
 Este método solo se admite en **nvarchar (max)**, **ntext**, y **xml** columnas. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Método updateNClob &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

