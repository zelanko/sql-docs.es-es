---
title: "Método setTrustStorePassword (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d42539e3a0979500c28539d256226624ac6997eb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>Método setTrustStorePassword (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece la contraseña que se usa para comprobar la integridad de los datos trustStore.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *trustStorePassword*  
  
 A **cadena** que contiene la contraseña que se usa para comprobar la integridad de los datos trustStore.  
  
## <a name="remarks"></a>Comentarios  
 La propiedad trustStorePassword se puede especificar junto con la propiedad trustStore y su valor se utiliza para comprobar la integridad del archivo trustStore.  
  
 Si se establece la propiedad trustStore pero no se establece la propiedad trustStorePassword, la integridad de trustStore no se comprueba.  
  
 Cuando las propiedades trustStore y trustStorePassword no se especifican, el controlador utilizará las propiedades del sistema de la máquina virtual Java (JVM), "javax.net.ssl.trustStore" y "javax.net.ssl.trustStorePassword". Si no se especifica la propiedad del sistema "javax.net.ssl.trustStorePassword", no se comprueba la integridad del trustStore.  
  
 Si no se establece la propiedad trustStore pero se establece la propiedad trustStorePassword, el controlador JDBC utilizará el archivo especificado por "javax.net.ssl.trustStore" como almacén de confianza y la integridad de éste se comprueba con la trustStorePassword especificada. Esto podría ser necesario cuando la aplicación cliente no desea almacenar la contraseña en la propiedad del sistema de JVM.  
  
 Para obtener más información, consulte [estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Desde el controlador JDBC 3.0, si establece SQLServerDataSource.setTrustStorePassword antes de enlazar las propiedades de origen de datos, deberá llamar a SQLServerDataSource.setTrustStorePassword antes de obtener la conexión. Para obtener más información, consulte [SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

