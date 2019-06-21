---
title: Método isWrapperFor (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 920e47391cbaaeb1e78c8a7a4f440880edab60fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803229"
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>Método isWrapperFor (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si este objeto es un contenedor para la interfaz especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *iface*  
  
 Un **clase** define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si este objeto implementa la interfaz o ajusta un objeto que implementa la interfaz. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) y el método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) se definen a través de la interfaz java.sql.Wrapper, que se incorpora en las especificaciones de JDBC 4.0.  
  
 Si este método devuelve el valor true, la llamada a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) con el mismo argumento se realizará correctamente.  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método Unwrap &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Miembros de clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
