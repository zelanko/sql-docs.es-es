---
title: Método setPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d102885fc235a66f5d42b7ae5100bc8905d895d2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788119"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>Método setPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el tamaño del paquete de red actual que se usa para establecer la comunicación con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y se especifica en bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *packetSize*  
  
 Valor **int** que contiene el tamaño del paquete de red.  
  
## <a name="remarks"></a>Notas  
 El rango de valores aceptables para esta propiedad es [-1 | 0 | 512..32767]. Si esta propiedad se establece en un valor fuera del rango aceptable, se produce una excepción.  
  
 Es posible que la aplicación desee establecer la propiedad packetSize mientras se conecta con el cifrado SSL (Capa de sockets seguros). El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] negocia el tamaño del paquete con el servidor. Si la propiedad de cifrado se establece en "**true**" y el tamaño del paquete negociado es mayor que el tamaño de registro SSL del proveedor de seguridad predeterminado de la máquina virtual Java (JVM), el controlador generará un error y finalizará la conexión.  
  
 Por otra parte, es posible que la aplicación desee establecer la propiedad packetSize sin solicitar el cifrado SSL. En este caso, si el servidor requiere que el cliente admita el cifrado SSL, el controlador comprueba el tamaño de registro de SSL del proveedor de seguridad predeterminado de la JVM. Si la propiedad packetSize es más grande que el tamaño de registro de SSL del proveedor de seguridad predeterminado de la JVM, el controlador generará un error y finalizará la conexión.  
  
 Para obtener más información sobre el uso de SSL, consulte [Using SSL Encryption](../../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
