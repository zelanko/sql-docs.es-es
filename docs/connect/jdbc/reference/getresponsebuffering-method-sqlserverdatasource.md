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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
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
  
 Para más información sobre cómo utilizar el modo de almacenamiento en búfer de respuesta, vea [Empleo de almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método setResponseBuffering &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
