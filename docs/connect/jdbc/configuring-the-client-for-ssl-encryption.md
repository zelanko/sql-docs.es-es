---
title: Configuración del cliente para el cifrado | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 123e847e01c07ab04bf5be97593af838abfdc4bd
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713286"
---
# <a name="configuring-the-client-for-encryption"></a>Configuración del cliente para el cifrado
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] o el cliente tienen que validar que el servidor es el correcto y que una entidad de certificación en la que el cliente confía ha emitido su certificado. Para validar el certificado de servidor, se debe proporcionar material de confianza en el momento de la conexión. Además, el emisor del certificado de servidor debe ser una entidad de certificación en la que el cliente confíe.  
  
 En este tema se describe primero cómo proporcionar el material de confianza en el equipo cliente. A continuación se describe cómo importar un certificado de servidor al almacén de confianza del equipo cliente cuando una entidad de certificación privada emita la instancia del certificado de seguridad de la capa de transporte (TLS) de SQL Server.  
  
 Para obtener más información sobre cómo validar el certificado de servidor, vea la sección Validar un certificado TLS de servidor en [Descripción de la compatibilidad con cifrado](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Configurar el almacén de confianza de cliente 
 La validación del certificado de servidor requiere que se suministre material de confianza en el momento de la conexión utilizando explícitamente las propiedades de conexión **trustStore** y **trustStorePassword**, o el almacén de confianza predeterminado de la máquina virtual Java (JVM) subyacente de forma implícita. Para obtener más información sobre cómo establecer las propiedades **trustStore** y **trustStorePassword** en una cadena de conexión, vea [Conexión con el cifrado](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Si la propiedad **trustStore** no se ha especificado o se ha establecido en null, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se basará en el proveedor de seguridad subyacente de JVM, la Extensión de sockets seguros de Java (SunJSSE, Java Secure Socket Extension). El proveedor de SunJSSE proporciona un TrustManager predeterminado, que se utiliza para validar los certificados X.509 que devuelve SQL Server con el material de confianza que se proporciona en un almacén de confianza.  
  
 El TrustManager intenta encontrar el trustStore predeterminado en el siguiente orden de búsqueda:  
  
-   Si la propiedad del sistema "javax.net.ssl.trustStore" está definida, TrustManager intenta buscar el archivo trustStore predeterminado con el nombre de archivo que especifica dicha propiedad del sistema.  
  
-   Si la propiedad del sistema "javax.net.ssl.trustStore" no se especificó, y si el archivo "\<java-home>/lib/security/jssecacerts" existe, se utiliza ese archivo.  
  
-   Si el archivo "\<java-home>/lib/security/cacerts" existe, se utiliza ese archivo.  
  
 Para obtener más información, consulte la documentación de la interfaz de SUNX509 TrustManager en el sitio web de Sun Microsystems.  
  
 El entorno de tiempo de ejecución de Java le permite establecer las propiedades del sistema trustStore y trustStorePassword como sigue:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 En este caso, cualquier aplicación que se ejecute en esta JVM utilizará estos valores como predeterminados. Para invalidar la configuración predeterminada de la aplicación, debería establecer las propiedades de conexión **trustStore** y **trustStorePassword** en la cadena de conexión o en el método de establecimiento adecuado de la clase [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Además, puede configurar y administrar los archivos de almacenes de confianza como "\<java-home>/lib/security/jssecacerts" y "\<java-home>/lib/security/cacerts". Para ello, utilice la utilidad JAVA "keytool" que se instala con el Entorno de tiempo de ejecución de Java (JRE, Java Runtime Environment). Para obtener más información sobre la utilidad "keytool", consulte la documentación de keytool en el sitio web de Sun Microsystems.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importar el certificado de servidor al almacén de confianza  
 Durante el protocolo de enlace TLS, el servidor envía su certificado de clave pública al cliente. El emisor de un certificado de clave pública se conoce como entidad de certificación (CA, Certificate Authority). El cliente tiene que asegurarse de que la entidad de certificación es una de aquellas en las que el cliente confía. Para ello, hay que saber de antemano la clave pública de las CA de confianza. Normalmente, la JVM incluye un conjunto predefinido de entidades de certificación de confianza.  
  
 Si una entidad de certificación privada emite la instancia del certificado TLS de SQL Server, debe agregar el certificado de la entidad de certificación a la lista de certificados de confianza en el almacén de confianza del equipo cliente.  
  
 Para ello, use la utilidad JAVA "keytool" que se instala con JRE. El símbolo del sistema siguiente muestra cómo utilizar la utilidad "keytool" para importar un certificado de un archivo:  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 El ejemplo utiliza un archivo denominado "caCert.cer" como archivo de certificado. Debe obtener este archivo de certificado del servidor. Los pasos siguientes explican cómo exportar el certificado de servidor a un archivo:  
  
1.  Haga clic en Inicio y, a continuación, en Ejecutar, y escriba MMC. (MMC es un acrónimo de Microsoft Management Console).  
  
2.  En MMC, abra Certificados.  
  
3.  Expanda Personal y Certificados.  
  
4.  Haga clic con el botón secundario del mouse en el certificado de servidor y, a continuación, seleccione Todas las tareas\Exportar.  
  
5.  Haga clic en Siguiente para pasar del cuadro de diálogo de bienvenida del Asistente para exportación de certificados.  
  
6.  Confirme que está seleccionada la opción "No, no exporte la clave privada" y, a continuación, haga clic en Siguiente.  
  
7.  Asegurarse de que están seleccionadas las opciones DER binario codificado X.509 (.CER) o X.509 codificado base-64 (.CER), y a continuación haga clic en Siguiente.  
  
8.  Escriba un nombre para el archivo de exportación.  
  
9. Haga clic en Siguiente y, a continuación, haga clic en Finalizar para exportar el certificado.  
  
## <a name="see-also"></a>Vea también  
 [Uso de cifrado](../../connect/jdbc/using-ssl-encryption.md)   
 [Protección de las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)