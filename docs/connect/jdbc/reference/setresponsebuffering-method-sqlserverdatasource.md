---
title: Método setResponseBuffering (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fa4e1c6921495448ce0a1e01a972b1786a69efd9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796755"
---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>Método setResponseBuffering (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el modo de almacenamiento en búfer de respuesta para las conexiones creadas mediante este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *value*  
  
 Un valor **String** que contiene el modo de almacenamiento en búfer y de transmisión por secuencias. El modo válido puede ser uno de los siguientes valores String que no distinguen mayúsculas de minúsculas: **full** o **adaptive**.  
  
## <a name="remarks"></a>Notas  
 El valor **full** se especifica mediante la lectura del resultado completo desde el servidor en el tiempo de ejecución.  
  
 El valor **adaptive** especifica que se almacenen en búfer los menos datos posibles cuando sea necesario. El valor **adaptive** es el modo de almacenamiento en búfer predeterminado.  
  
 Para obtener más información sobre cómo usar el modo de almacenamiento en búfer de respuesta, consulte [usando almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
