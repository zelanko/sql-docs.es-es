---
title: Método setPacketSize (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08f4f72aae10fc154b7362a83e870d85b9fb42e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32844610"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>Método setPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el tamaño de paquete de red actual que se utiliza para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], especificado en bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Tamaño del paquete*  
  
 Un **int** valor que contiene el tamaño de paquete de red.  
  
## <a name="remarks"></a>Comentarios  
 El rango de valores aceptables para esta propiedad es [-1 | 0 | 512..32767]. Si esta propiedad se establece en un valor fuera del rango aceptable, se produce una excepción.  
  
 Es posible que la aplicación desee establecer la propiedad packetSize mientras se conecta con el cifrado SSL (Capa de sockets seguros). El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] negocia el tamaño del paquete con el servidor. Si la propiedad encrypt se establece en "**true**" y el tamaño del paquete negociado es mayor que el tamaño del registro SSL del proveedor de seguridad de la máquina Virtual Java (JVM) de manera predeterminada, el controlador generará un error y terminará la conexión.  
  
 Por otra parte, es posible que la aplicación desee establecer la propiedad packetSize sin solicitar el cifrado SSL. En este caso, si el servidor requiere que el cliente admita el cifrado SSL, el controlador comprueba el tamaño de registro de SSL del proveedor de seguridad predeterminado de la JVM. Si la propiedad packetSize es más grande que el tamaño de registro de SSL del proveedor de seguridad predeterminado de la JVM, el controlador generará un error y finalizará la conexión.  
  
 Para obtener más información sobre el uso de SSL, consulte [utilizando cifrado SSL](../../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
