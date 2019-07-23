---
title: Método isWrapperFor (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c35cad678ce4f9b6008b656302d4767bad9b1244
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977062"
---
# <a name="iswrapperfor-method-sqlserverstatement"></a>Método isWrapperFor (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si este objeto de instrucción es un contenedor para la interfaz especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *iface*  
  
 Una **clase** que define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si este objeto implementa la interfaz o ajusta un objeto que implementa la interfaz. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) y el método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) se definen a través de la interfaz java.sql.Wrapper, que se incorpora en JDBC 4.0.  
  
 Si este método devuelve el valor true, la llamada a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) con el mismo argumento se realizará correctamente.  
  
 Para obtener un ejemplo de código, vea el [ejemplo de actualización de datos de gran tamaño](../../../connect/jdbc/updating-large-data-sample.md).  
  
 Para obtener más información, vea [contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Unwrap ( &#40;método) SQLServerStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
