---
title: Method setSQLXML (SQLServerCallableStatement) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: de095cb3-1111-4154-8996-3c2e529e3000
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcc2c813c0c2f52872938ae09134f20664c7097c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setsqlxml-method-sqlservercallablestatement"></a>Method setSQLXML (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto especificado de SQLXML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setSQLXML(java.lang.String parameterName,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Un **cadena** que indica el nombre del parámetro.  
  
 *xmlObject*  
  
 Un objeto SQLXML que contiene el valor del parámetro.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setSQLXML es especificado por el método setSQLXML en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
