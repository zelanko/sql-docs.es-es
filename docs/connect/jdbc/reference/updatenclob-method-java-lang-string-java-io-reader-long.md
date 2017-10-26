---
title: "Método updateNClob (java.lang.String, java.io.Reader, long) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad5c8d9b-f8c8-4ddf-85c8-23420bba54ee
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d4ff78e585d2d5751e3cebfbbd7df7f8881dff4f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updatenclob-method-javalangstring-javaioreader-long"></a>Método updateNClob (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada mediante especificado **lector** objeto, que es el número especificado de caracteres de longitud.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 A **cadena** que indica la etiqueta de columna.  
  
 *lector*  
  
 Un objeto de lector.  
  
 *length*  
  
 El número de caracteres en los datos del parámetro.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateNClob especificado por el método updateNClob en la interfaz java.sql.ResultSet.  
  
 Este método solo se admite en **nvarchar (max)**, **ntext**, y **xml** columnas. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Método updateNClob &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

