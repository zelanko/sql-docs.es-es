---
title: Método getURL (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb709f6b-64e1-4d0c-a704-290891627dd7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: add077cc98e9453b5523c816ff9c47b67a13272c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779819"
---
# <a name="geturl-method-javalangstring"></a>Método getURL (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto URL en el lenguaje de programación Java según el nombre del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.net.URL getURL(java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *s*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de dirección URL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getURL especifica este método getURL en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método getURL &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
