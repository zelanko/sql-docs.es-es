---
title: Method setSQLXML (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: de095cb3-1111-4154-8996-3c2e529e3000
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 21a32b48eb3c00d7163dd9eda93e8bd971fe99e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66791726"
---
# <a name="setsqlxml-method-sqlservercallablestatement"></a>Method setSQLXML (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto SQLXML especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setSQLXML(java.lang.String parameterName,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Un objeto **String** que indica el nombre del parámetro.  
  
 *xmlObject*  
  
 Un objeto SQLXML que contiene el valor del parámetro.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método setSQLXML especifica este método setSQLXML en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
