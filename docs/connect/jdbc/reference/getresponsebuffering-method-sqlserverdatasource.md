---
title: Método getResponseBuffering (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getResponseBuffering()
apilocation:
- SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4b3e53579b8c95cce0585e9614152053f39cafa8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980436"
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>Método getResponseBuffering (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el método de almacenamiento en búfer de respuesta para este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto **String** que contiene un atributo **full** o **adaptive** en minúscula.  
  
## <a name="remarks"></a>Observaciones  
 El valor **full** se especifica mediante la lectura del resultado completo desde el servidor en el tiempo de ejecución.  
  
 El valor **adaptive** especifica que se almacenen en búfer los menos datos posibles cuando sea necesario. El valor **adaptive** es el modo de almacenamiento en búfer predeterminado.  
  
 Para más información sobre cómo utilizar el modo de almacenamiento en búfer de respuesta, consulte [Empleo de almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método setResponseBuffering &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
