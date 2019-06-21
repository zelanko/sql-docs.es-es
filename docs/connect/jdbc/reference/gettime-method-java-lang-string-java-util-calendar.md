---
title: Método getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6b9d74778d3ff1fc62b5549fbea7e0f97bf1e477
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778880"
---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>Método getTime (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Time en el lenguaje de programación Java según el nombre de parámetro y usando el objeto Calendar determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *cal*  
  
 Un objeto de calendario.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de tiempo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getTime especifica este método getTime en la interfaz java.sql.CallableStatement.  
  
 Vea el gráfico titulado "Conversiones de métodos de captador" en [descripción de las conversiones de tipo de datos](../../../connect/jdbc/understanding-data-type-conversions.md) para ver qué [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos se pueden recuperar con este método.  
  
## <a name="see-also"></a>Consulte también  
 [Método getTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
