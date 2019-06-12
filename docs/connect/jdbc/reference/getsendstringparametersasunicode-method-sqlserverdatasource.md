---
title: Método getSendStringParametersAsUnicode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88f5d294e46ddc6dc4da92e437fc4513f9a50a47
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792005"
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>Método getSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **boolean** que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si se envían parámetros de cadena al servidor en formato UNICODE. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad sendStringParametersAsUnicode está configurada en **true**, que es el valor predeterminado, los parámetros de cadena se envían al servidor en formato UNICODE. Si la propiedad sendStringParametersAsUnicode está configurada en **false**, los parámetros de cadena se envían al servidor en formato ASCII/MBCS y no en UNICODE. Si no se establece sendStringParametersAsUnicode, getSendStringParametersAsUnicode devuelve el valor predeterminado **true**.  
  
 Para obtener más información acerca de la propiedad de conexión sendStringParametersAsUnicode, vea [estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
