---
title: Método setBinaryStream para el flujo de entrada) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 339c8277-2d08-4094-9fa9-26c8ad3e7348
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04a286c4d6c8b44482c254e7fe30b84836283df0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975134"
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream"></a>Método setBinaryStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el flujo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Valor **string** que contiene el nombre del parámetro.  
  
 *x*  
  
 Objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setBinaryStream se especifica mediante el método setBinaryStream de la interfaz java. SQL. CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [setBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
