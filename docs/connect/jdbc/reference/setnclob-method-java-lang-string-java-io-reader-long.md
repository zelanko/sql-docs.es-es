---
title: Método setNClob (java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c1b95ee7-7e82-418f-8f30-948589086f63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1af4961609b132ebf6b508b54386e4c02ee3e6e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850083"
---
# <a name="setnclob-method-javalangstring-javaioreader-long"></a>Método setNClob (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto Reader especificado, que es el número de caracteres indicado para la longitud.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.io.Reader reader,  
              long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *reader*  
  
 Un objeto lector.  
  
 *length*  
  
 Un valor **long** que indica el número de caracteres en el flujo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método se debe usar para **NCHAR**, **NVARCHAR**, **NTEXT**, y **XML** tipos de datos de parámetro.  
  
 El método setNClob especifica este método setNClob en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Ver también  
 [Método setNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
