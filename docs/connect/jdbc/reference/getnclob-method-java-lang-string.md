---
title: Método getNClob (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b95a22911f1b7e49f6310e9c06a7ea4ef4a899fa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784455"
---
# <a name="getnclob-method-javalangstring"></a>Método getNClob (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro JDBC **NCLOB** designado como un objeto en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 ANClobobject.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getNClob especifica este método getNClob en la interfaz java.sql.CallableStatement.  
  
 Este método solo admite la recuperación **NCHAR**, **NVARCHAR**, **NTEXT**, y **XML** parámetros. Si estos métodos se llaman en otros parámetros del tipo de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
