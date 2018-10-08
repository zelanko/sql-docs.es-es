---
title: Método getPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30b2387b4685440de737ad9e6be7d351ded86506
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736643"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Método getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el número de puerto actual que se utiliza para la comunicación con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **int** que contiene el número de puerto actual.  
  
## <a name="remarks"></a>Notas  
 El número de puerto es el número del puerto TCP/IP que se utiliza al abrir una conexión de socket con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece la propiedad portNumber, el método getPortNumber devuelve el valor predeterminado de 1433.  
  
> [!NOTE]  
>  El [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) método no realiza ninguna comprobación en el pasado en el valor del puerto del intervalo. Puede pasar números erróneos que no son válidos como 99999, sin desencadenar un error.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
