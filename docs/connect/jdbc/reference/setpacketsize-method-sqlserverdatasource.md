---
title: "Método setPacketSize (SQLServerDataSource) | Documentos de Microsoft"
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
apiname: SQLServerDataSource.setPacketSize
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aca0de41e907beb56752838554bb6c752b25e96f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>Método setPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el tamaño de paquete de red actual que se utiliza para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], especificado en bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *tamaño del paquete*  
  
 Un **int** valor que contiene el tamaño de paquete de red.  
  
## <a name="remarks"></a>Comentarios  
 El rango de valores aceptables para esta propiedad es [-1 | 0 | 512..32767]. Si esta propiedad se establece en un valor fuera del rango aceptable, se produce una excepción.  
  
 Es posible que la aplicación desee establecer la propiedad packetSize mientras se conecta con el cifrado SSL (Capa de sockets seguros). El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] negocia el tamaño del paquete con el servidor. Si la propiedad encrypt se establece en "**true**" y el tamaño del paquete negociado es mayor que el tamaño del registro SSL del proveedor de seguridad de la máquina Virtual Java (JVM) de manera predeterminada, el controlador generará un error y terminará la conexión.  
  
 Por otra parte, es posible que la aplicación desee establecer la propiedad packetSize sin solicitar el cifrado SSL. En este caso, si el servidor requiere que el cliente admita el cifrado SSL, el controlador comprueba el tamaño de registro de SSL del proveedor de seguridad predeterminado de la JVM. Si la propiedad packetSize es más grande que el tamaño de registro de SSL del proveedor de seguridad predeterminado de la JVM, el controlador generará un error y finalizará la conexión.  
  
 Para obtener más información sobre el uso de SSL, consulte [utilizando cifrado SSL](../../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
