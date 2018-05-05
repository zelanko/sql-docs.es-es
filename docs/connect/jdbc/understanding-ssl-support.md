---
title: Descripción de la compatibilidad con SSL | Documentos de Microsoft
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
ms.openlocfilehash: 089ec1a4a16f9a0568bda9aa584948fd4704ae5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-ssl-support"></a>Descripción de la compatibilidad con SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], si la aplicación solicita cifrado y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para admitir el cifrado SSL, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] inicia el protocolo de enlace SSL. El protocolo de enlace permite al servidor y al cliente negociar los algoritmos criptográficos y de cifrado que se usarán para proteger los datos. Después de completar el protocolo de enlace SSL, el cliente y el servidor pueden enviar los datos cifrados de forma segura. Durante el protocolo de enlace SSL, el servidor envía su certificado de clave pública al cliente. El emisor de un certificado de clave pública se conoce como entidad de certificación (CA, Certificate Authority). El cliente es responsable de validar que la entidad de certificación sea una en la que el cliente confíe.  
  
 Si la aplicación no solicita cifrado, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no exigirá que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para admitir el cifrado SSL. Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia no está configurada para exigir el cifrado SSL, se establece una conexión sin cifrado. Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia está configurada para exigir el cifrado SSL, el controlador habilitará automáticamente el cifrado SSL cuando se ejecuta en Máquina Virtual configurada correctamente Java (JVM) o else se termina la conexión y el controlador generará un error.  
  
> [!NOTE]  
>  Asegúrese de que el valor pasado a **serverName** coincide exactamente con el nombre DNS o nombre común (CN) en el nombre alternativo sujeto (SAN) en el certificado de servidor para una conexión SSL sea correcta.  
  
> [!NOTE]  
>  Para obtener más información acerca de cómo configurar SSL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte cifrar conexiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="remarks"></a>Comentarios  
 Para permitir que las aplicaciones usen el cifrado SSL, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] presenta las siguientes propiedades de conexión a partir de la versión 1.2: **cifrar**, **trustServerCertificate**, **trustStore**, **trustStorePassword**, y **hostNameInCertificate**. Para obtener más información, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 La tabla siguiente resume cómo el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se comporta la versión para posibles escenarios de conexión de SSL. Cada escenario usa un conjunto diferente de propiedades de conexión SSL. La tabla incluye:  
  
-   **en blanco**: "la propiedad no existe en la cadena de conexión"  
  
-   **valor**: "la propiedad existe en la cadena de conexión y su valor es válido"  
  
-   **cualquier**: "No importa si la propiedad existe en la cadena de conexión o su valor no es válido"  
  
> [!NOTE]  
>  El mismo comportamiento se aplica para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación de usuario y la autenticación integrada de Windows.  
  
|encrypt|trustServerCertificate|hostNameInCertificate|trustStore|trustStorePassword|Comportamiento|  
|-------------|----------------------------|---------------------------|----------------|------------------------|--------------|  
|false o en blanco|cualquiera|cualquiera|cualquiera|cualquiera|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no exigirá que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para admitir el cifrado SSL. Si el servidor tiene un certificado autofirmado, el controlador inicia el intercambio del certificado SSL. El certificado SSL no será validado y solo se cifran las credenciales (en el paquete de inicio de sesión).<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL, el controlador iniciará el intercambio de certificados SSL. El certificado SSL no será validado, pero se cifrará toda la comunicación.|  
|true|true|cualquiera|cualquiera|cualquiera|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL. Tenga en cuenta que si el **trustServerCertificate** propiedad se establece en "true", el controlador no validará el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|en blanco|en blanco|en blanco|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **serverName** propiedad especificada en la dirección URL de conexión para validar el certificado SSL del servidor y se basan en reglas de búsqueda del generador del Administrador de confianza para determinar qué almacén de certificado que se va a usar.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|value|en blanco|en blanco|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador validará el valor del sujeto del certificado SSL con el valor especificado para la **hostNameInCertificate** propiedad.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|en blanco|value|value|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **trustStore** valor de propiedad para buscar el archivo trustStore del certificado y **trustStorePassword** valor de propiedad para comprobar la integridad del archivo trustStore.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|en blanco|en blanco|value|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **trustStorePassword** valor de propiedad para comprobar la integridad del archivo trustStore predeterminado.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|en blanco|value|en blanco|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **trustStore** valor de propiedad para buscar la ubicación del archivo trustStore.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|value|en blanco|value|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **trustStorePassword** valor de propiedad para comprobar la integridad del archivo trustStore predeterminado. Además, el controlador utilizará el **hostNameInCertificate** valor de propiedad para validar el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|value|value|en blanco|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **trustStore** valor de propiedad para buscar la ubicación del archivo trustStore. Además, el controlador utilizará el **hostNameInCertificate** valor de propiedad para validar el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
|true|false o en blanco|value|value|value|El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitudes para usar el cifrado SSL con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Si el servidor requiere que el cliente sea compatible con el cifrado SSL o si admite el cifrado, el controlador iniciará el intercambio de certificados SSL.<br /><br /> El controlador utilizará el **trustStore** valor de propiedad para buscar el archivo trustStore del certificado y **trustStorePassword** valor de propiedad para comprobar la integridad del archivo trustStore. Además, el controlador utilizará el **hostNameInCertificate** valor de propiedad para validar el certificado SSL.<br /><br /> Si el servidor no está configurado para ser compatible con el cifrado SSL, el controlador generará un error y terminará la conexión.|  
  
 Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa el proveedor de JVM predeterminado JSSE seguridad para negociar el cifrado SSL con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. El proveedor de seguridad predeterminado puede no admitir todas las características necesarias para negociar el cifrado SSL correctamente. Por ejemplo, el proveedor de seguridad predeterminado puede no admitir el tamaño de la clave pública RSA utilizada en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL. En este caso, el proveedor de seguridad predeterminado podría generar un error que ocasionará que el controlador JDBC termine la conexión. Para resolver este problema, intente una de las siguientes acciones:  
  
-   Configurar la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con un certificado de servidor que tiene una clave pública RSA más pequeña  
  
-   Configurar la JVM para usar un proveedor de seguridad JSSE diferente en el "\<java-home > / lib/security/java.security" archivo de propiedades de seguridad  
  
-   Usar una JVM distinta  
  
## <a name="validating-server-ssl-certificate"></a>Validar un certificado SSL de servidor  
 Durante el protocolo de enlace SSL, el servidor envía su certificado de clave pública al cliente. El controlador JDBC o el cliente tienen que validar que una entidad de certificación en la que el cliente confíe emita el certificado de servidor. El controlador requiere que el certificado de servidor cumpla las condiciones siguientes:  
  
-   Una entidad de certificación de confianza emita el certificado.  
  
-   El certificado debe ser emitido para la autenticación de servidor.  
  
-   El certificado no ha expirado.  
  
-   El nombre común (CN) en el asunto o un nombre DNS en el nombre alternativo sujeto (SAN) del certificado coincide exactamente con el **serverName** valor especificado en la cadena de conexión o, si no se especifica, el  **hostNameInCertificate** valor de propiedad.  
  
-   Un nombre DNS puede incluir caracteres comodín. Pero la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no admite la coincidencia de carácter comodín. Es decir, abc.com no coincidirá con *.com pero \*coincidirá con .com \*. com.  
  
## <a name="see-also"></a>Vea también  
 [Está utilizando cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
