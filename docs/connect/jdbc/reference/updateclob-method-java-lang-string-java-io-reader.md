---
title: "Método updateClob (java.lang.String, java.io.Reader) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 338a2bf2-b110-469d-ad08-a0f2bbefcb88
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0522c6435f89efb35dbd93d1f0be4ac345f44023
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="updateclob-method-javalangstring-javaioreader"></a>Método updateClob (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada mediante el objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateClob(java.lang.String columnLabel,  
                        java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 A **cadena** que contiene la etiqueta de columna.  
  
 *lector*  
  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateClob especificado por el método updateClob en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Método updateClob &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
