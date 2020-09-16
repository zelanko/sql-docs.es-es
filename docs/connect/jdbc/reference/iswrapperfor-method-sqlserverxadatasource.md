---
description: Método isWrapperFor (SQLServerXADataSource)
title: Método isWrapperFor (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: caab887a8e104313f78a593520ea7d735008fd1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433297"
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
  
 Una **clase** que define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si este objeto implementa la interfaz o encapsula un objeto que implementa la interfaz. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) y el método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) se definen a través de la interfaz java.sql.Wrapper, que se incorpora en las especificaciones de JDBC 4.0.  
  
 Si este método devuelve el valor true, la llamada a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) con el mismo argumento se realizará correctamente.  
  
 Para más información, consulte [Contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método unwrap &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Miembros de clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
