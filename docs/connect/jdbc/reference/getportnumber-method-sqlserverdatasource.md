---
title: "Método getPortNumber (SQLServerDataSource) | Documentos de Microsoft"
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
apiname: SQLServerDataSource.getPortNumber
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ab9d426cea1048f7902af97c68951347c12e16d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Método getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el número de puerto actual que se usa para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** valor que contiene el número de puerto actual.  
  
## <a name="remarks"></a>Comentarios  
 El número de puerto es el número de puerto TCP/IP que se utiliza al abrir una conexión de socket a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Si no se establece la propiedad portNumber, el método getPortNumber devuelve el valor predeterminado de 1433.  
  
> [!NOTE]  
>  El [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) método no realiza ninguna comprobación en el valor del puerto pasado del intervalo. Puede pasar números erróneos que no son válidos, como 99999, sin que se desencadene un error.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
