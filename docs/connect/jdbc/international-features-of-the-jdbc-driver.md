---
title: Características internacionales del controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 321176cae5783968826f3094f63a5c6e30a1d3e9
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601975"
---
# <a name="international-features-of-the-jdbc-driver"></a>Características internacionales del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Entre las características de internacionalización de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se incluye lo siguiente:  
  
-   Compatibilidad con el trabajo en los mismos idiomas que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Compatibilidad con las conversiones de idioma de Java para datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] susceptibles a la configuración regional  
  
-   Compatibilidad con idiomas internacionales, independientemente del sistema operativo  
  
-   Compatibilidad con nombres de dominio internacionales (a partir de Microsoft JDBC Driver 6.0 para SQL Server)  
  
## <a name="handling-of-character-data"></a>Tratamiento de datos de caracteres  
 Los datos de caracteres en Java se tratan de forma predeterminada como Unicode, el objeto **String** de Java representa datos de caracteres Unicode. En el controlador JDBC, la única excepción a esta regla son los métodos establecedor y captador de flujos ASCII, que son casos especiales porque usan flujos de bytes con la presunción implícita de páginas de códigos únicas conocidas (ASCII).  
  
 Además, el controlador JDBC proporciona la **sendStringParametersAsUnicode** propiedad cadena de conexión. Esta propiedad se puede usar para especificar que los parámetros preparados para los datos de caracteres se envíen como ASCII o juego de caracteres multibyte (MBCS) en lugar de Unicode. Para obtener más información sobre la **sendStringParametersAsUnicode** propiedad de cadena de conexión, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
### <a name="driver-incoming-conversions"></a>Conversiones entrantes en el controlador  
 Los datos de texto Unicode que provengan del servidor no necesitan conversión. Se pasan directamente como Unicode. Los datos que no sean Unicode y provengan del servidor se convierten de una página de códigos de datos, en el nivel de la base de datos o de columna, a Unicode. El controlador JDBC emplea las rutinas de conversión de la Máquina Virtual Java (JVM) para realizar estas conversiones. Estas conversiones se realizan en todos los métodos establecedores de flujos String y Character.  
  
 Si la JVM no posee la compatibilidad adecuada de la página de códigos para los datos de la base de datos, el controlador JDBC lanza la excepción "la página de códigos XXX no es compatible con el entorno Java". Para solucionar este problema, debería instalar la compatibilidad completa con caracteres internacionales necesaria para esa JVM. Como ejemplo, vea la documentación relativa a las codificaciones compatibles (Supported Encodings) en el sitio web de Sun Microsystems.  
  
### <a name="driver-outgoing-conversions"></a>Conversiones salientes del controlador  
 Los datos de caracteres que vayan desde el controlador hasta el servidor pueden ser ASCII o Unicode. Por ejemplo, los nuevos métodos de caracteres nacionales de JDBC 4.0 (como los métodos setNString, setNCharacterStream y setNClob de las clases [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)) siempre envían sus valores de parámetro al servidor en formato Unicode.  
  
 Por otra parte, los métodos API de caracteres no nacionales (como los métodos setString, setCharacterStream y setClob de las clases [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)) envían sus valores al servidor de Unicode solamente cuando la propiedad **sendStringParametersAsUnicode** está establecida en "true", que es el valor predeterminado.  
  
## <a name="non-unicode-parameters"></a>Parámetros que no son Unicode  
 Para obtener un rendimiento óptimo con **CHAR**, **VARCHAR** o **LONGVARCHAR** del tipo de parámetros que no son Unicode, establezca el **sendStringParametersAsUnicode** conexión propiedad string que "false" y usar los métodos de caracteres nacionales.  
  
## <a name="formatting-issues"></a>Problemas de formato  
 En cuanto a la fecha, la hora y las divisas, el formato con datos localizados se aplica en el nivel de lenguaje Java empleando el objeto Locale y los diversos métodos de formato correspondientes a los tipos de datos **Date**, **Calendar** y **Number**. En el caso excepcional en el que el controlador JDBC debe pasar datos para los que el idioma sea importante en un formato localizado, se utiliza el formateador correspondiente con la configuración regional predeterminada de la JVM.  
  
## <a name="collation-support"></a>Compatibilidad con intercalación  
 El controlador JDBC 3.0 admite todas las intercalaciones compatibles con [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], así como las nuevas intercalaciones o nuevas versiones de los nombres de intercalación de Windows que se incluyeron en [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
 Para más información sobre las intercalaciones, vea [Compatibilidad con la intercalación y Unicode](https://go.microsoft.com/fwlink/?LinkId=131366) y [Nombre de intercalación de Windows (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=131367) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-international-domain-names-idn"></a>Usar nombres de dominio internacionales (IDN)  
 JDBC Driver 6.0 para SQL Server admite el uso de nombres de dominio internacionalizados (IDN) y puede convertir un nombre de servidor Unicode en codificación compatible con ASCII (Punycode) cuando sea necesario durante una conexión.  Si los IDN se almacenan en el sistema de nombres de dominio (DNS) como cadenas ASCII en el formato Punycode (especificado por RFC 3490), habilite la conversión del nombre de servidor Unicode al establecer la propiedad serverNameAsACE en true.  De lo contrario, si el servicio DNS está configurado para permitir el uso de caracteres Unicode, establezca la propiedad serverNameAsACE en false (valor predeterminado).  En versiones anteriores del controlador JDBC, también es posible convertir el valor de serverName en Punycode mediante los métodos [IDN.toASCII de Java](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) antes de establecer la propiedad de una conexión.  
  
> [!NOTE]  
>  La mayoría del software de resolver escrito para plataformas distintas de Windows se basa en los estándares DNS de Internet y, por tanto, es probable que use el formato Punycode para los IDN, mientras que un servidor de DNS basado en Windows en una red privada se puede configurar para permitir el uso de caracteres UTF-8 según el servidor.  Para más información, vea [Compatibilidad con caracteres Unicode](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx).  
  
## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
