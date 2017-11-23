---
title: "Método isWrapperFor (SQLServerStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c9ddb7aab2cad2a7acd4f5cf685df5f5fff674a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
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
  
 A **clase** define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si este objeto implementa la interfaz o contiene un objeto que implementa la interfaz. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 El [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) método y [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) método se definen mediante la interfaz java.sql.Wrapper, que se incorpora en JDBC 4.0.  
  
 Si este método devuelve true, la llamada a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) con el mismo argumento se realizará correctamente.  
  
 Para un código de ejemplo, vea [muestra de datos grandes actualización](../../../connect/jdbc/updating-large-data-sample.md).  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Unwrap (método) &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
