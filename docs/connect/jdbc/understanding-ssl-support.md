---
title: Descripción de la compatibilidad con SSL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed75ab57adf1ffb11a9da0d332c3524601e0230a
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662327"
---
# <a name="understanding-ssl-support"></a>Descripción de la compatibilidad con SSL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Al conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], si la aplicación solicita cifrado y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurada para admitir el cifrado SSL, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] inicia el protocolo de enlace SSL. El protocolo de enlace permite al servidor y al cliente negociar los algoritmos criptográficos y de cifrado que se usarán para proteger los datos. Después de completar el protocolo de enlace SSL, el cliente y el servidor pueden enviar los datos cifrados de forma segura. Durante el protocolo de enlace SSL, el servidor envía su certificado de clave pública al cliente. El emisor de un certificado de clave pública se conoce como entidad de certificación (CA, Certificate Authority). El cliente es responsable de validar que la entidad de certificación sea una en la que el cliente confíe.  
  
Si la aplicación no solicita cifrado, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no exige a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que admita el cifrado SSL. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no está configurada para exigir el cifrado SSL, se establece una conexión sin cifrado. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurada para exigir el cifrado SSL, el controlador habilita automáticamente el cifrado SSL cuando se ejecuta en una máquina virtual Java (JVM) configurada correctamente; de lo contrario, se finaliza la conexión y el controlador genera un error.  
  
> [!NOTE]  
> Asegúrese de que el valor pasado a **serverName** coincida exactamente con el nombre común (CN) o con el nombre DNS del nombre alternativo de sujeto (SAN) del certificado de servidor para que la conexión SSL se establezca correctamente.  
>
> Para obtener más información sobre cómo configurar SSL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], vea el tema Cifrar conexiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="remarks"></a>Notas

Con el fin de permitir que las aplicaciones usen el cifrado SSL, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] incorpora las siguientes propiedades de conexión a partir de la versión 1.2: **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** y **hostNameInCertificate**. Para obtener más información, vea [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 En la tabla siguiente se resume cómo se comporta la versión de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] en los posibles escenarios de conexión SSL. Cada escenario usa un conjunto diferente de propiedades de conexión SSL. La tabla incluye:  
  
- **en blanco**: "la propiedad no existe en la cadena de conexión"  
  
- **valor**: "la propiedad existe en la cadena de conexión y su valor es válido"  
  
- **cualquier**: "No importa si la propiedad existe en la cadena de conexión o su valor no es válido"  
  
> [!NOTE]  
> El mismo comportamiento se aplica para la autenticación de usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y la autenticación integrada de Windows.  
  
| encrypt        | trustServerCertificate | hostNameInCertificate | trustStore | trustStorePassword | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ---------------------- | --------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| false o en blanco | cualquiera                    | cualquiera                   | cualquiera        | cualquiera                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no obliga a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] admita el cifrado SSL. Si el servidor tiene un certificado autofirmado, el controlador inicia el intercambio del certificado SSL. El certificado SSL no será validado y solo se cifran las credenciales (en el paquete de inicio de sesión).<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL, el controlador iniciará el intercambio de certificados SSL. El certificado SSL no será validado, pero se cifrará toda la comunicación.                                                                                                                                                                                    |
| true           | true                   | cualquiera                   | cualquiera        | cualquiera                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL. Observe que si la propiedad **trustServerCertificate** se establece en "true", el controlador no valida el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                                                                                                                                          |
| true           | false o en blanco         | en blanco                 | en blanco      | en blanco              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa la propiedad **serverName** especificada en la dirección URL de conexión para validar el certificado SSL de servidor y confía en las reglas de búsqueda del generador del administrador de confianza con el fin de determinar qué almacén de certificados se va a usar.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                             |
| true           | false o en blanco         | value                 | en blanco      | en blanco              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador valida el valor del asunto del certificado SSL con el valor especificado para la propiedad **hostNameInCertificate**.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                                                                                                                 |
| true           | false o en blanco         | en blanco                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa el valor de la propiedad **trustStore** para buscar el archivo trustStore del certificado y el valor de la propiedad **trustStorePassword** para comprobar la integridad del archivo trustStore.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                                                                |
| true           | false o en blanco         | en blanco                 | en blanco      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa el valor de la propiedad **trustStorePassword** para comprobar la integridad del archivo trustStore predeterminado.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                                                                                                                                  |
| true           | false o en blanco         | en blanco                 | value      | en blanco              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa el valor de la propiedad **trustStore** para buscar la ubicación del archivo trustStore.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                                                                                                                                                 |
| true           | false o en blanco         | value                 | en blanco      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa el valor de la propiedad **trustStorePassword** para comprobar la integridad del archivo trustStore predeterminado. Además, el controlador usa el valor de la propiedad **hostNameInCertificate** para validar el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                   |
| true           | false o en blanco         | value                 | value      | en blanco              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa el valor de la propiedad **trustStore** para buscar la ubicación del archivo trustStore. Además, el controlador usa el valor de la propiedad **hostNameInCertificate** para validar el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.                                                                                  |
| true           | false o en blanco         | value                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicita usar cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador usa el valor de la propiedad **trustStore** para buscar el archivo trustStore del certificado y el valor de la propiedad **trustStorePassword** para comprobar la integridad del archivo trustStore. Además, el controlador usa el valor de la propiedad **hostNameInCertificate** para validar el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión. |
  
Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa el proveedor de seguridad JSSE predeterminado de JVM para negociar el cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. El proveedor de seguridad predeterminado puede no admitir todas las características necesarias para negociar el cifrado SSL correctamente. Por ejemplo, es posible que el proveedor de seguridad predeterminado no admita el tamaño de la clave pública RSA que se usa en el certificado SSL de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. En este caso, el proveedor de seguridad predeterminado podría generar un error que ocasionará que el controlador JDBC termine la conexión. Para resolver este problema, intente una de las siguientes acciones:  
  
- Configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con un certificado de servidor que tenga una clave pública RSA más pequeña  
  
- Configurar la JVM para usar un proveedor de seguridad JSSE diferente en el archivo de propiedades de seguridad "\<java-home>/lib/security/java.security"  
  
- Usar una JVM distinta  
  
## <a name="validating-server-ssl-certificate"></a>Validar un certificado SSL de servidor  

Durante el protocolo de enlace SSL, el servidor envía su certificado de clave pública al cliente. El controlador JDBC o el cliente tienen que validar que una entidad de certificación en la que el cliente confíe emita el certificado de servidor. El controlador requiere que el certificado de servidor cumpla las condiciones siguientes:  
  
- Una entidad de certificación de confianza emita el certificado.  
  
- El certificado debe haberse emitido para la autenticación de servidor.  
  
- El certificado no ha expirado.  
  
- El nombre común (CN) del asunto o un nombre DNS del nombre alternativo de sujeto (SAN) del certificado debe coincidir exactamente con el valor **serverName** especificado en la cadena de conexión o, si se ha especificado, con el valor de la propiedad **hostNameInCertificate**.  
  
- Un nombre DNS puede incluir caracteres comodín. Pero [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no admite la coincidencia de caracteres comodín. Es decir, abc.com no coincide con *.com, pero \*.com sí coincide con \*.com.  
  
## <a name="see-also"></a>Ver también

[Usar el cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)

[Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
