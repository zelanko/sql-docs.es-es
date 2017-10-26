---
title: "Método getSendStringParametersAsUnicode (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 520e40a43f47536b34ef68ebebde73f199c8e915
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>Método getSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un **booleano** valor que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se envían parámetros string al servidor en formato UNICODE. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Comentarios  
 Si se establece la propiedad sendStringParametersAsUnicode en **true**, que es el valor predeterminado, se envían parámetros string al servidor en formato UNICODE. Si sendStringParametersAsUnicode se establece en **false**, se envían parámetros string al servidor en formato ASCII/MBCS, pero no en UNICODE. Si no se establece sendStringParametersAsUnicode, getSendStringParametersAsUnicode devuelve el valor predeterminado de **true**.  
  
 Para obtener más información acerca de la propiedad de conexión sendStringParametersAsUnicode, vea [estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

