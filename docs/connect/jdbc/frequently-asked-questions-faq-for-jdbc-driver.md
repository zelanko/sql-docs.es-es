---
title: "Preguntas más frecuentes (P+F para el controlador JDBC) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508f8526ed13af3f7f92aa500b182e077f5bb23d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Preguntas más frecuentes (P+F para el controlador JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En este artículo se ofrecen respuestas a las preguntas más frecuentes sobre Microsoft JDBC Driver for SQL Server.  
  
## <a name="frequently-asked-questions"></a>Preguntas más frecuentes  
**¿Cómo puedo ayudar a mejorar el controlador JDBC?**  
El controlador JDBC es código abierto y el código fuente puede encontrarse en [GitHub](https://github.com/microsoft/mssql-jdbc). Puede ayudar a mejorar el controlador de envío de problemas y que contribuyen a la base de código.

**¿Qué versiones de SQL Server y Java admite el controlador?**  
 Consulte la [Microsoft JDBC Driver para SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) página para obtener más información.  
  
 **¿Qué debo saber al actualizar el controlador?**  
 El 6.2 de controlador JDBC de Microsoft es compatible con las especificaciones de JDBC 4.0, 4.1 y 4.2 e incluye dos bibliotecas de clases JAR en el paquete de instalación como se indica a continuación:  
  
|JAR|Especificación de JDBC|Versión JDK|  
|-|-|-|  
|MSSQL-jdbc-6.2.1.jre8.jar|JDBC 4.0, 4.1 y 4.2|JDK 8.0|  
|MSSQL-jdbc-6.2.1.jre7.jar|JDBC 4.1 y 4.0|JDK 7.0|  
 
 Microsoft JDBC Drivers 6.0 y 4.2 para SQL Server admite especificaciones de JDBC 4.0, 4.1 y 4.2 e incluyen dos bibliotecas de clases JAR en el paquete de instalación como se indica a continuación:  
  
|JAR|Especificación de JDBC|Versión JDK|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.0, 4.1 y 4.2|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 y 4.0|JDK 7.0|  
  
 Microsoft JDBC Driver 4.1 para SQL Server es compatible con la especificación de JDBC 4.0 y se incluye una biblioteca de clases JAR en el paquete de instalación como se indica a continuación:  
  
|JAR|Especificación de JDBC|Versión JDK|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 y 6.0|
  
 Microsoft JDBC Driver 4.0 para SQL Server admite especificaciones de JDBC 3.0 y JDBC 4.0 e incluye dos bibliotecas de clases de archivo JAR en el paquete de instalación (una por cada especificación: sqljdbc.jar y sqljdbc4.jar respectivamente).  
  
|JAR|Especificación de JDBC|Versión JDK|   
|-|-|-|  
|sqljdbc4.jar|JDBC 4.0|JDK 6.0 y 5.0|  
|sqljdbc.jar|JDBC 3.0|JDK 6.0 y 5.0|  
  
 **¿Es necesario realizar ningún cambio de código de mi aplicación para usar el controlador más reciente con mi versión de SQL Server existente?**  
 Por lo general, el controlador lo diseñamos para que sea compatible con versiones anteriores, así que no es necesario cambiar las aplicaciones existentes al actualizar el controlador. En caso de que una nueva versión de controlador presenta un cambio importante, el [notas de la versión para el controlador JDBC](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) sección proporcionará saber con claridad en el cambio y el impacto en las aplicaciones existentes. Además, puede consultar las notas de la versión incluidas con el controlador para obtener una lista de errores corregidos en esa versión y problemas conocidos.  
  
 **¿Cuánto cuesta el controlador?**  
 Microsoft JDBC Driver for SQL Server está disponible sin ningún coste adicional.  
  
 **¿Se puede redistribuir el controlador?** Los controladores JDBC 4.1, 4.2, 6.0 y 6.2 son redistribuibles. Revise la cláusula "Código distribuible" en los contratos de licencia.
 
 El controlador JDBC 4.0 es puede redistribuir libremente mediante una licencia de redistribución independiente que obliga a registrarse. Para registrar o para obtener más información, consulte nuestro [redistribuir Microsoft JDBC Driver](../../connect/jdbc/redistributing-the-microsoft-jdbc-driver.md). 
 
   
 **¿Puedo usar el controlador para tener acceso a Microsoft SQL Server desde un equipo Linux?** Sí. Puede utilizar el controlador para acceder a SQL Server desde otras plataformas distintas de Windows, Unix y Linux. Consulte nuestro [Microsoft JDBC Driver para SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) para obtener más detalles.  
  
 **¿El controlador admite el cifrado de capa de Sockets seguros (SSL)?** A partir de la versión 1.2, el controlador admite el cifrado de capa de sockets seguros (SSL). Para obtener más información, consulte [utilizando cifrado SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
 **¿Qué tipos de autenticación son compatibles con el controlador JDBC de Microsoft para SQL Server?**  
 En la tabla siguiente se muestran las opciones de autenticación disponibles. Tenga en cuenta que la autenticación Kerberos pura de Java está disponible a partir de la versión 4.0 del controlador.  
  
|||  
|-|-|  
|Plataforma|Autenticación|  
|Distinta de Windows|Kerberos pura de Java|  
|Distinta de Windows|SQL Server|  
|Windows|Kerberos pura de Java|  
|Windows|SQL Server|  
|Windows|Kerberos con copia de seguridad NTLM|  
|Windows|NTLM|  
  
**¿El controlador es compatible con protocolo de Internet versión 6 (IPv6) direcciones?**  
 Sí. El controlador admite el uso de direcciones IPv6 con la colección de propiedades de conexión y la propiedad de cadena de conexión serverName. Para obtener más información, consulte [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).  
  
**¿Qué es el almacenamiento en búfer adaptable?**  
 El almacenamiento en búfer adaptable se introdujo a partir de Microsoft JDBC Driver 1.2 para SQL Server 2005 y está diseñado para recuperar cualquier tipo de datos de valor grande sin la sobrecarga de cursores del servidor. La característica de almacenamiento en búfer adaptable de Microsoft SQL Server JDBC Driver proporciona una propiedad de cadena de conexión, responseBuffering, cuyos valores puede establecerse en "adaptive" o "full". A partir de Microsoft JDBC Driver 2.0, el comportamiento predeterminado del controlador es "adaptive". Dicho de otro modo, para obtener el comportamiento de almacenamiento en búfer adaptable, su aplicación no tiene que solicitar explícitamente el comportamiento adaptable. No obstante, en la versión 1.2, el modo del almacenamiento en búfer era "full" de manera predeterminada y la aplicación tenía que solicitar el modo de almacenamiento en búfer adaptable explícitamente. Para obtener más información, consulte [usar almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md) tema y el blog de [qué Adaptive almacena en búfer y por qué debo usarlo?](http://go.microsoft.com/fwlink/?LinkId=111575).  
  
**¿Es la agrupación de conexiones de compatibilidad de controlador?**  
 El controlador proporciona compatibilidad con la agrupación de conexiones de Java Platform, Enterprise Edition 5 (Java EE 5). El controlador implementa las interfaces necesarias de JDBC 3.0 para que pueda participar en la implementación de la agrupación de conexiones de los proveedores de servidores de aplicaciones de software intermedio. El controlador participa en las conexiones agrupadas en estos entornos. Para obtener más información, consulte [Using Connection Pooling](../../connect/jdbc/using-connection-pooling.md). El controlador no proporciona su propia implementación de agrupación, sino que se basa en servidores de aplicaciones Java de terceros.  
  
**¿Hay soporte técnico para el controlador?**  
 Existen varias opciones de soporte. Puede publicar su pregunta o emitir a nuestro [repositorio de GitHub](https://github.com/microsoft/mssql-jdbc) que está supervisada por Microsoft. [Foros](http://go.microsoft.com/fwlink/?LinkID=246673) están supervisados por Microsoft, MVP y la Comunidad. También puede ponerse en contacto con el equipo de asistencia al cliente de Microsoft. Es posible que le pidamos que reproduzca el problema fuera de los servidores de aplicaciones de terceros. Si el problema no se puede reproducir fuera del entorno de contenedor host de Java, tendrá que ponerse en contacto con el tercero relacionado para que podamos seguir ayudándolo. También puede que le pidamos que reproduzca el problema en un sistema operativo concreto, como Windows, para que podamos ofrecerle la mejor ayuda posible.  
  
**¿Es el controlador certificado para su uso con los servidores de aplicaciones de terceros?**
El controlador se ha probado con los principales servidores de aplicaciones, incluidos IBM WebSphere y SAP NetWeaver.  
  
**¿Cómo habilitar el seguimiento?**  
 El controlador admite el uso del seguimiento (o registro) para ayudar a solucionar problemas con Microsoft JDBC Driver cuando se esté utilizando en su aplicación. Para habilitar el uso de seguimiento de archivos JAR del lado cliente, Microsoft JDBC Driver utiliza las API de registro de java.util.logging. Para obtener más información, consulte [funcionamiento del controlador de seguimiento](../../connect/jdbc/tracing-driver-operation.md). Para el seguimiento de archivos XA del lado servidor, consulte [Data Access Tracing in SQL Server](http://go.microsoft.com/fwlink/?LinkId=248705)(Seguimiento de datos de acceso en SQL Server).  
  
**¿Dónde puedo descargar versiones anteriores del controlador como el controlador JDBC de SQL Server 2000, 2005 controlador, 1.0, 1.1 y 1.2 del controlador?**  
 Estas versiones del controlador no están disponibles para descargarse debido a que ya no son compatibles. Estamos trabajando continuamente para mejorar la compatibilidad con la conectividad de Java. Por tanto, se recomienda encarecidamente trabajar con la versión más reciente de Microsoft JDBC Driver.  
  
 **Uso JRE 1.4. ¿Qué controlador es compatible con JRE 1.4** para los clientes que utilizan productos SAP y requieren compatibilidad con JRE 1.4, pueden ponerse en contacto [SAPService Marketplace](http://service.sap.com/) para obtener Microsoft JDBC driver 1.2.  
  
**¿El controlador, que puede comunicarse mediante algoritmos aprobados en FIPS?** Microsoft JDBC Driver no contiene algoritmos criptográficos. Si un cliente utiliza algoritmos de sistemas operativos, aplicaciones y JVM que el estándar federal de procesamiento de información (FIPS) considera aceptables y configura el controlador para usar esos algoritmos, el controlador utilizará solo los designados para la comunicación.  
  
  

