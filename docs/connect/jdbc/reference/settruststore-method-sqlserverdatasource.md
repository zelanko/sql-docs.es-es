---
title: Método setTrustStore (SQLServerDataSource) | Documentos de Microsoft
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
ms.topic: article
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b12bef0614e06bbc47458b3284b09eb66f6e1b87
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="settruststore-method-sqlserverdatasource"></a>Método setTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece la ruta de acceso (incluido el nombre de archivo) del archivo trustStore del certificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *trustStore*  
  
 A **cadena** que contiene la ruta de acceso (incluido el nombre de archivo) en el archivo trustStore del certificado.  
  
## <a name="remarks"></a>Comentarios  
 Si la propiedad trustStore está especificado o está establecida en null, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se basará en reglas para determinar qué almacén de certificados para usar de búsqueda del generador del Administrador de confianza. El generador TrustManagerFactory SunX509 predeterminado intenta buscar material de confianza en las ubicaciones siguientes en este orden:  
  
-   1. Un archivo especificado por la propiedad del sistema "javax.net.ssl.trustStore" de la máquina virtual Java (JVM).  
  
-   2. "\<java-home >/lib/security/jssecacerts" archivo.  
  
-   3. "\<java-home >/lib/security/cacerts" archivo.  
  
 Para obtener más información, consulte la documentación de la interfaz de SunX509 TrustManager en el sitio web de Sun Microsystems.  
  
 Si la propiedad trustStore está establecida en una cadena o en una cadena vacía "", el controlador utilizará ese valor para buscar el archivo trustStore con el fin de validar el certificado SSL del servidor.  
  
 La propiedad trustStorePassword se puede especificar junto con la propiedad trustStore y su valor se utiliza para abrir el archivo trustStore. Para obtener más información, consulte [setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
