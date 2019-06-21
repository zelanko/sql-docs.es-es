---
title: Método isWrapperFor (SQLServerConnectionPoolDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 09ed10eb-6e46-437b-a7c0-3c55574aad38
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9d85327897da4e4c677eaf036ea067ccb9c549b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796264"
---
# <a name="iswrapperfor-method-sqlserverconnectionpooldatasource"></a>Método isWrapperFor (SQLServerConnectionPoolDataSource)
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
 El método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) y el método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) se definen a través de la interfaz java.sql.Wrapper, que se incorpora en las especificaciones de JDBC 4.0.  
  
 Si este método devuelve el valor true, la llamada a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) con el mismo argumento se realizará correctamente.  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)   
 [Métodos SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Miembros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Clase SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
