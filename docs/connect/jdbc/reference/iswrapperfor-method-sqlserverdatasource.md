---
title: Método isWrapperFor (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5dbf1b4159d060fce122455436a3ff7b7199e583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796306"
---
# <a name="iswrapperfor-method-sqlserverdatasource"></a>Método isWrapperFor (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si este objeto de origen de datos es un contenedor para la interfaz especificada.  
  
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
 El método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md) y el método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) se definen a través de la interfaz java.sql.Wrapper, que se incorpora en las especificaciones de JDBC 4.0.  
  
 Si este método devuelve el valor true, la llamada a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) con el mismo argumento se realizará correctamente.  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método Unwrap &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
