---
title: Método getDouble (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8eab6a8e-91f3-47b1-8707-5e57368ad0c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4d248f06bac0f57f7fdd79e11eab482cb8bcb3ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66765996"
---
# <a name="getdouble-method-javalangstring"></a>Método getDouble (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto **double** en el lenguaje de programación Java según el nombre del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public double getDouble(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **doble** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getDouble especifica este método getDouble en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve todos los tipos de datos basados en número con fidelidad **double** de Java.  
  
## <a name="see-also"></a>Consulte también  
 [Método getDouble &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
