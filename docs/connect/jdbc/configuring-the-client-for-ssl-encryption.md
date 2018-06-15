---
title: Configuración del cliente para el cifrado SSL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7a45a0da57be9df27d205b644e1d7156151982f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832549"
---
# <a name="configuring-the-client-for-ssl-encryption"></a>Configurar el cliente para el cifrado SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] o el cliente tiene que validar que el servidor es el servidor correcto y su certificado emitido por una entidad emisora de certificados que el cliente confíe. Para validar el certificado de servidor, se debe proporcionar material de confianza en el momento de la conexión. Además, el emisor del certificado de servidor debe ser una entidad de certificación en la que el cliente confíe.  
  
 En este tema se describe primero cómo proporcionar el material de confianza en el equipo cliente. A continuación se describe cómo importar un certificado de servidor al almacén de confianza del equipo cliente cuando una entidad de certificación privada emita la instancia del certificado de Capa de sockets seguros (SSL) de SQL Server.  
  
 Para obtener más información sobre cómo validar el certificado de servidor, vea la sección de validación de certificado de servidor SSL en [descripción de la compatibilidad SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Configurar el almacén de confianza de cliente  
 Validar el certificado de servidor requiere que se debe proporcionar material de confianza en tiempo de conexión mediante **trustStore** y **trustStorePassword** propiedades de conexión explícitamente, o mediante usar el almacén de confianza de forma predeterminada el subyacente Máquina Virtual Java (JVM) del implícitamente. Para obtener más información sobre cómo establecer el **trustStore** y **trustStorePassword** propiedades en una cadena de conexión, consulte [conectarse con el cifrado SSL](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Si el **trustStore** propiedad es no especificado o está establecida en null, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se basará en el proveedor de seguridad subyacente de JVM, la extensión de sockets seguros de Java (SunJSSE). El proveedor de SunJSSE proporciona un predeterminado TrustManager, que se utiliza para validar certificados X.509 devueltos por SQL Server en el material de confianza proporcionado en un almacén de confianza.  
  
 El elemento TrustManager intenta encontrar el trustStore predeterminado en el siguiente orden de búsqueda:  
  
-   Si se define la propiedad del sistema "javax.net.ssl.trustStore", el TrustManager intenta encontrar el archivo trustStore predeterminado mediante el nombre de archivo especificado por dicha propiedad del sistema.  
  
-   Si no se especificó la propiedad del sistema "javax.net.ssl.trustStore" y el archivo "\<java-home >/lib/security/jssecacerts" existe, se utiliza ese archivo.  
  
-   Si el archivo "\<java-home >/lib/security/cacerts" existe, se utiliza ese archivo.  
  
 Para obtener más información, consulte la documentación de la interfaz de SUNX509 TrustManager en el sitio web de Sun Microsystems.  
  
 El entorno de tiempo de ejecución de Java le permite establecer las propiedades del sistema trustStore y trustStorePassword como sigue:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 En este caso, cualquier aplicación que se ejecute en esta JVM utilizará estos valores como predeterminados. Para invalidar la configuración predeterminada de la aplicación, debe establecer el **trustStore** y **trustStorePassword** propiedades de conexión en la cadena de conexión o en los correspondientes método de establecedor de la [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) clase.  
  
 Además, puede configurar y administrar los archivos de almacén de confianza predeterminados como "\<java-home >/lib/security/jssecacerts" y "\<java-home >/lib/security/cacerts". Para ello, utilice la utilidad JAVA "keytool" que se instala con el Entorno de tiempo de ejecución de Java (JRE, Java Runtime Environment). Para obtener más información sobre la utilidad "keytool", consulte la documentación de keytool en el sitio web de Sun Microsystems.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importar el certificado de servidor al almacén de confianza  
 Durante el protocolo de enlace SSL, el servidor envía su certificado de clave pública al cliente. El emisor de un certificado de clave pública se conoce como entidad de certificación (CA, Certificate Authority). El cliente tiene que asegurarse de que la entidad de certificación es una de aquellas en las que el cliente confía. Para ello, hay que saber de antemano la clave pública de las CA de confianza. Normalmente, la JVM incluye un conjunto predefinido de entidades de certificación de confianza.  
  
 Si una entidad de certificación privada emite la instancia del certificado SSL de SQL Server, debe agregar el certificado de la entidad de certificación a la lista de certificados de confianza en el almacén de confianza del equipo cliente.  
  
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
 [Está utilizando cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
