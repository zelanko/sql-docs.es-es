---
title: "Características internacionales del controlador JDBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
caps.latest.revision: "40"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f323a5728aa9f63ba5283a34694c1e00baa0bb91
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="international-features-of-the-jdbc-driver"></a>Características internacionales del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Las características de internacionalización de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] incluyen lo siguiente:  
  
-   Compatibilidad para una experiencia totalmente localizada en los mismos idiomas que[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Compatibilidad con las conversiones de idioma de Java para la configuración regional confidencial [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] datos  
  
-   Compatibilidad con idiomas internacionales, independientemente del sistema operativo  
  
-   Compatibilidad con nombres de dominio internacionales (a partir de Microsoft JDBC Driver 6.0 para SQL Server)  
  
## <a name="handling-of-character-data"></a>Tratamiento de datos de caracteres  
 Datos de caracteres en Java se tratan como Unicode de forma predeterminada; el Java **cadena** objeto representa datos de caracteres Unicode. En el controlador JDBC, la única excepción a esta regla son los métodos establecedor y captador de flujos ASCII, que son casos especiales porque usan flujos de bytes con la presunción implícita de páginas de códigos únicas conocidas (ASCII).  
  
 Además, el controlador JDBC proporciona la **sendStringParametersAsUnicode** propiedad cadena de conexión. Esta propiedad se puede usar para especificar que los parámetros preparados para los datos de caracteres se envíen como ASCII o juego de caracteres multibyte (MBCS) en lugar de Unicode. Para obtener más información sobre la **sendStringParametersAsUnicode** propiedad de cadena de conexión, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
### <a name="driver-incoming-conversions"></a>Conversiones entrantes en el controlador  
 Los datos de texto Unicode que provengan del servidor no necesitan conversión. Se pasan directamente como Unicode. Los datos que no sean Unicode y provengan del servidor se convierten de una página de códigos de datos, en el nivel de la base de datos o de columna, a Unicode. El controlador JDBC emplea las rutinas de conversión de la Máquina Virtual Java (JVM) para realizar estas conversiones. Estas conversiones se realizan en todos los métodos establecedores de flujos String y Character.  
  
 Si la JVM no posee la compatibilidad adecuada de la página de códigos para los datos de la base de datos, el controlador JDBC lanza la excepción "la página de códigos XXX no es compatible con el entorno Java". Para solucionar este problema, debería instalar la compatibilidad completa con caracteres internacionales necesaria para esa JVM. Como ejemplo, vea la documentación relativa a las codificaciones compatibles (Supported Encodings) en el sitio web de Sun Microsystems.  
  
### <a name="driver-outgoing-conversions"></a>Conversiones salientes del controlador  
 Los datos de caracteres que vayan desde el controlador hasta el servidor pueden ser ASCII o Unicode. Por ejemplo, los nuevos JDBC 4.0 caracteres no nacionales métodos, como métodos setNString, setNCharacterStream y setNClob de [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clases, Enviar siempre sus valores de parámetro para el servidor de Unicode.  
  
 Por otro lado, los métodos de API de caracteres no nacionales, como métodos setString y setCharacterStream, setClob de [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clases enviar sus valores para el servidor de Unicode solamente cuando el **sendStringParametersAsUnicode** propiedad se establece en "true", que es el valor predeterminado.  
  
## <a name="non-unicode-parameters"></a>Parámetros que no son Unicode  
 Para obtener un rendimiento óptimo con **CHAR**, **VARCHAR** o **LONGVARCHAR** tipo de parámetros no es Unicode, establezca la **sendStringParametersAsUnicode** conexión propiedad en "false" de la cadena y utilizar los métodos de caracteres nacionales.  
  
## <a name="formatting-issues"></a>Problemas de formato  
 Para fecha, hora y divisas, todo el formato con datos localizados se realiza en el nivel de lenguaje Java mediante el objeto de configuración regional; y los diversos métodos de formato para **fecha**, **calendario**, y **número** tipos de datos. En el caso excepcional en el que el controlador JDBC debe pasar datos para los que el idioma sea importante en un formato localizado, se utiliza el formateador correspondiente con la configuración regional predeterminada de la JVM.  
  
## <a name="collation-support"></a>Compatibilidad con intercalación  
 El controlador JDBC 3.0 admite todas las intercalaciones compatibles con [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]y las nuevas intercalaciones o nuevas versiones de Windows, los nombres de intercalación que se introducen en [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
 Para obtener más información acerca de las intercalaciones, vea [Collation and Unicode Support](http://go.microsoft.com/fwlink/?LinkId=131366) y [nombre de intercalación de Windows (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=131367) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="using-international-domain-names-idn"></a>Usar nombres de dominio internacionales (IDN)  
 El controlador JDBC 6.0 para SQL Server admite el uso de nombres de dominio internacionalizados (IDN) y puede convertir un nombre de servidor de Unicode en codificación compatible con ASCII (Punycode) cuando sea necesario durante una conexión.  Si los IDN se almacenan en el sistema de nombres de dominio (DNS) como cadenas ASCII en el formato Punycode (especificado por RFC 3490), habilite la conversión del nombre de servidor Unicode al establecer la propiedad serverNameAsACE en true.  De lo contrario, si el servicio DNS está configurado para permitir el uso de caracteres Unicode, establezca la propiedad serverNameAsACE en false (valor predeterminado).  Para versiones anteriores del controlador JDBC, también es posible convertir el valor de serverName en Punycode mediante [IDN.toASCII de Java](http://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) métodos antes de establecer la propiedad para una conexión.  
  
> [!NOTE]  
>  La mayoría del software de resolver escrito para plataformas distintas de Windows se basa en los estándares DNS de Internet y, por tanto, es probable que use el formato Punycode para los IDN, mientras que un servidor de DNS basado en Windows en una red privada se puede configurar para permitir el uso de caracteres UTF-8 según el servidor.  Para obtener más información, consulte [compatibilidad con caracteres Unicode](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx).  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
