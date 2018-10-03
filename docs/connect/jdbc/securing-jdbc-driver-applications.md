---
title: Protección de aplicaciones del controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42fed21bd2857ea9305b1b8f8771aff80ee9f2ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600413"
---
# <a name="securing-jdbc-driver-applications"></a>Proteger las aplicaciones del controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La mejora de la seguridad de una aplicación de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] conlleva algo más que evitar los errores de codificación comunes. Una aplicación que tiene acceso a los datos tiene muchos puntos de error potenciales que un atacante puede aprovechar para recuperar, manipular o destruir información confidencial. Es importante entender todos los aspectos de seguridad, desde el proceso de modelado de amenazas durante la fase de diseño de una aplicación a su implementación final, y continuarlo durante su mantenimiento continuado.  
  
En los temas de esta sección se describen algunos orígenes de problemas de seguridad comunes como son las cadenas de conexión, la validación de los datos proporcionados por el usuario y la seguridad general de las aplicaciones.  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                            | Descripción                                                                                                                                                           |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Proteger las cadenas de conexión](../../connect/jdbc/securing-connection-strings.md) | Describe técnicas para ayudar a proteger la información que se usa para conectarse a un origen de datos.                                                                                    |
| [Validación de los datos proporcionados por el usuario](../../connect/jdbc/validating-user-input.md)             | Describe técnicas para validar los datos proporcionados por el usuario.                                                                                                                          |
| [Seguridad de aplicaciones](../../connect/jdbc/application-security.md)               | Describe cómo utilizar los permisos de las directivas de Java para ayudar a proteger una aplicación del controlador JDBC.                                                                                |
| [Usar el cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)               | Describe cómo establecer un canal de comunicación seguro con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante Capa de sockets seguros (SSL). |
| [Modo FIPS](../../connect/jdbc/fips-mode.md)                                     | Describe cómo usar el controlador JDBC en el modo compatible con FIPS.                                                                                                              |
  
## <a name="see-also"></a>Ver también  

 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
