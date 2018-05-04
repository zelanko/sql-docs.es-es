---
title: Proteger aplicaciones del controlador JDBC | Documentos de Microsoft
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
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d777abfd88a6218e96ab1054d175f4e24e3b59d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="securing-jdbc-driver-applications"></a>Proteger las aplicaciones del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Mejorar la seguridad de un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicación implica más que evitar los errores de codificación comunes. Una aplicación que tiene acceso a los datos tiene muchos puntos de error potenciales que un atacante puede aprovechar para recuperar, manipular o destruir información confidencial. Es importante entender todos los aspectos de seguridad, desde el proceso de modelado de amenazas durante la fase de diseño de una aplicación a su implementación final, y continuarlo durante su mantenimiento continuado.  
  
 En los temas de esta sección se describen algunos orígenes de problemas de seguridad comunes como son las cadenas de conexión, la validación de los datos proporcionados por el usuario y la seguridad general de las aplicaciones.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Proteger las cadenas de conexión](../../connect/jdbc/securing-connection-strings.md)|Describe técnicas para ayudar a proteger la información que se usa para conectarse a un origen de datos.|  
|[Validación de los datos proporcionados por el usuario](../../connect/jdbc/validating-user-input.md)|Describe técnicas para validar los datos proporcionados por el usuario.|  
|[Seguridad de aplicaciones](../../connect/jdbc/application-security.md)|Describe cómo utilizar los permisos de las directivas de Java para ayudar a proteger una aplicación del controlador JDBC.|  
|[Usar el cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)|Describe cómo establecer un canal de comunicaciones seguro con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante capa de Sockets seguros (SSL) de la base de datos.|  
|[Modo FIPS](../../connect/jdbc/fips-mode.md)|Describe cómo usar el controlador JDBC en el modo compatible con FIPS.| 
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
