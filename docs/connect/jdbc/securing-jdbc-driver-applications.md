---
title: Proteger aplicaciones del controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8033e1690fcaa01ca73ce1a7d0d9972ac2d3ba9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="securing-jdbc-driver-applications"></a>Proteger las aplicaciones del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Mejorar la seguridad de un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicación implica más que evitar los errores de codificación comunes. Una aplicación que tiene acceso a los datos tiene muchos puntos de error potenciales que un atacante puede aprovechar para recuperar, manipular o destruir información confidencial. Es importante entender todos los aspectos de seguridad, desde el proceso de modelado de amenazas durante la fase de diseño de una aplicación a su implementación final, y continuarlo durante su mantenimiento continuado.  
  
 En los temas de esta sección se describen algunos orígenes de problemas de seguridad comunes como son las cadenas de conexión, la validación de los datos proporcionados por el usuario y la seguridad general de las aplicaciones.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Proteger las cadenas de conexión](../../connect/jdbc/securing-connection-strings.md)|Describe técnicas para ayudar a proteger la información que se usa para conectarse a un origen de datos.|  
|[Validar la entrada del usuario](../../connect/jdbc/validating-user-input.md)|Describe técnicas para validar los datos proporcionados por el usuario.|  
|[Seguridad de la aplicación](../../connect/jdbc/application-security.md)|Describe cómo utilizar los permisos de las directivas de Java para ayudar a proteger una aplicación del controlador JDBC.|  
|[Está utilizando cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)|Describe cómo establecer un canal de comunicaciones seguro con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante capa de Sockets seguros (SSL) de la base de datos.|  
|[Modo FIPS](../../connect/jdbc/fips-mode.md)|Describe cómo usar el controlador JDBC en el modo FIPS denunciante.| 
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
