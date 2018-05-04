---
title: Método setSendStringParametersAsUnicode (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18a2f401fb19d1ac90cc5fb1f7f685c03f02919a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>Método setSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un **booleano** valor que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sendStringParametersAsUnicode*  
  
 **True** si se envían parámetros string al servidor en formato UNICODE. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Comentarios  
 Si se establece la propiedad sendStringParametersAsUnicode en **true**, que es el valor predeterminado, se envían parámetros string al servidor en formato UNICODE. Si sendStringParametersAsUnicode se establece en **false** se envían parámetros string al servidor en formato ASCII/MBCS, pero no en UNICODE. Si no se establece sendStringParametersAsUnicode, [getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) devuelve el valor predeterminado de **true**.  
  
 Para obtener más información acerca de la propiedad de conexión sendStringParametersAsUnicode, vea [estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
