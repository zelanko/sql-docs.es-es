---
title: "Problemas de diseño de seguridad de ADO | Documentos de Microsoft"
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51c7e3cf9c99bdd76ce1b84a7c387b1e6e4d2f58
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="ado-security-design-features"></a>Características de diseño de seguridad de ADO
En las siguientes secciones se describen las características de diseño de seguridad de ActiveX Data Objects (ADO) 2,8 y versiones posteriores. Estos cambios se realizaron en ADO 2.8 para mejorar la seguridad. ADO 6.0, que se incluye en Windows DAC 6.0 en Windows Vista, es funcionalmente equivalente a ADO 2.8, que se incluye en MDAC 2.8 en Windows XP y Windows Server 2003. Este tema proporciona información acerca de cómo proteger mejor sus aplicaciones en ADO 2.8 o versiones posterior.

> [!IMPORTANT]
>  Si va a actualizar su aplicación desde una versión anterior de ADO, se recomienda que pruebe la aplicación actualizada en un equipo que no sea de producción antes de implementarla en los clientes. De esta manera, puede asegurarse de que es conscientes de los problemas de compatibilidad antes de implementar la aplicación actualizada.

## <a name="internet-explorer-file-access-scenarios"></a>Escenarios de acceso de archivo de Internet Explorer
 El siguiente efecto de características el funcionamiento de ADO 2,8 y versiones posteriores cuando se utiliza en un script de páginas Web en Internet Explorer.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Cuadro de mensaje de advertencia de seguridad mejorada y revisado usar ahora para avisar a los usuarios
 Para ADO 2.7 y versiones anterior, aparece el siguiente mensaje de advertencia cuando una página Web mediante scripts intenta ejecutar código ADO de un proveedor de confianza:

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Para ADO 2,8 y versiones posteriores, ya no aparece el mensaje anterior. En su lugar, aparece el mensaje siguiente en este contexto:

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 El mensaje anterior permite al usuario tomar una decisión informada, sabiendo las consecuencias de ambas opciones:

-   Si el usuario confía en el sitio, haga clic en Aceptar permitirá todo el código seguro para el disco (todos los métodos de ADO y propiedades con las excepciones de las API accesible para el disco que se describe más adelante en este tema) para ejecutar y se ejecutan en la ventana del explorador.

-   Si el usuario no confía en el sitio, haga clic en Cancelar bloquea el código de ADO para el acceso de datos de ejecución y ejecutar en su totalidad.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Código accesible para el disco limitado ahora a sitios de confianza
 Se realizaron cambios de diseño adicionales en ADO 2.8 que restringir específicamente la capacidad de un conjunto limitado de API, lo que pueden exponer la posibilidad de leer o escribir en archivos en el equipo local. Estos son los métodos de API que han estado más restringido por motivos de seguridad cuando se ejecuta Internet Explorer:

-   Para la propiedad ADO **flujo** objeto, si la [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) o [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) se usan los métodos.

-   Para ADO **conjunto de registros** objeto, si el valor la [guardar](../../ado/reference/ado-api/save-method.md) método o la [abierto](../../ado/reference/ado-api/open-method-ado-recordset.md) método, por ejemplo, cuando cualquier la **adCmdFile** opción está establecida o el [proveedor Microsoft OLE DB persistencia (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) se utiliza.

 Para estos conjunto limitado de funciones potencialmente accesibles en disco, ocurre lo siguiente para ADO 2,8 y versiones posterior, si cualquier código que utilice estos métodos se ejecuta en Internet Explorer:

-   Si el sitio que proporciona el código se ha agregado anteriormente a la lista de la zona de sitios de confianza, el código se ejecuta en el explorador y se concede acceso a archivos locales.

-   Si el sitio no aparece en la lista de la zona de sitios de confianza, el código se bloquea y se deniega el acceso a archivos locales.

    > [!NOTE]
    >  En ADO 2,8 y versiones posterior, el usuario no es una alerta o se recomienda agregar sitios a la lista de la zona de sitios de confianza. Por lo tanto, la administración de la lista de sitios de confianza es la responsabilidad de los destinatarios que se va a implementar o compatibles con sitios Web basados en aplicaciones que requieren acceso al sistema de archivos local.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Acceso bloqueado a la propiedad ActiveCommand en objetos de conjunto de registros
 Cuando se ejecuta en Internet Explorer, ADO 2.8 ahora bloquea el acceso a la [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) propiedad para un activo **Recordset** de objetos y devuelve un error. El error se produce independientemente de si la página procede de un sitio Web que se registra en la lista de sitios de confianza.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Cambios en el control para proveedores OLE DB y la seguridad integrada
 Al revisar ADO 2.7 y las versiones anteriores de posibles problemas de seguridad y problemas, se detectó el siguiente escenario:

 En algunos casos, los proveedores de OLE DB que admiten la seguridad integrada [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) propiedad potencialmente podría permitir que las páginas Web con secuencias de comandos para volver a usar el objeto de conexión ADO para conectarse de forma no intencionada a otros servidores con las credenciales de inicio de sesión actual de los usuarios. Para evitar esto, ADO 2,8 y versiones posteriores controlan los proveedores de OLE DB, dependiendo de cómo ha elegido para proporcionar o no se proporciona, para la seguridad integrada.

 Para las páginas Web que se cargan desde sitios que se indican en la lista de la zona de sitios de confianza, en la tabla siguiente proporciona un desglose de cómo ADO 2,8 y versiones posteriores administra las conexiones de ADO en cada caso.

|Configuración de Internet Explorer para la autenticación de usuario de inicio de sesión|Admite el proveedor "Integrated Security" y UID y PWD están especificados (SQLOLEDB)|Proveedor no admite "Integrated Security" (JOLT, MSDASQL, MSPersist)|Proveedor admite "Integrated Security" y se establece en SSPI (no se especifica ningún UID y PWD)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Inicio de sesión automático con el nombre de usuario actual y la contraseña|Permitir la conexión|Permitir la conexión|Permitir la conexión|
|Símbolo del sistema de nombre de usuario y contraseña|Permitir la conexión|Un error de conexión|Un error de conexión|
|Inicio de sesión automático solo en la zona de Intranet|Permitir la conexión|Solicitar al usuario con una advertencia de seguridad|Solicitar al usuario con una advertencia de seguridad|
|Inicio de sesión anónimo|Permitir la conexión|Un error de conexión|Un error de conexión|

 En el caso de una advertencia de seguridad donde aparece el cuadro de mensaje informa a los usuarios:

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 El mensaje anterior permite al usuario tomar una decisión más informada y actúe en consecuencia.

> [!NOTE]
>  Para los sitios de confianza (es decir, los sitios no aparecen en la lista de la zona de sitios de confianza), si el proveedor también es de confianza (como se ha descrito anteriormente en esta sección), el usuario puede ver dos advertencias de seguridad en una fila, una advertencia sobre el proveedor no seguro y una segunda advertencia acerca de la intentó usar su identidad. Si el usuario hace clic en Aceptar para la primera advertencia, se ejecutan la configuración de Internet Explorer y el código de comportamiento de respuesta se describe en la tabla anterior.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Controlar si el texto de la contraseña se devuelve en las cadenas de conexión de ADO
 Al intentar obtener el valor de la [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad ADO **conexión** objeto, ocurre lo siguiente:

1.  Si la conexión está abierta, una llamada de inicialización, a continuación, se realiza con el proveedor OLE DB subyacente para obtener la cadena de conexión.

2.  Dependiendo de la configuración en el proveedor OLE DB de la [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) propiedad, las contraseñas se incluyen junto con otra información de la cadena de conexión que se devuelve.

 Por ejemplo, si la propiedad dinámica de conexión ADO **Persist Security Info** está establecido en **True**, información de contraseña se incluye en la cadena de conexión devuelta. En caso contrario, si el proveedor subyacente ha establecido la propiedad en **False** (por ejemplo, con el proveedor SQLOLEDB), se omite la información de contraseña en la cadena de conexión devuelta.

 Si usas aplicaciones de terceros (es decir, no son de Microsoft) proveedores de OLE DB con el código de aplicación de ADO, debe comprobar cómo el **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** propiedad se implementa para determinar si la inclusión de se permite la información de contraseña con cadenas de conexión de ADO.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Comprobación de los dispositivos no sean de archivo al cargar y guardar los conjuntos de registros o secuencias
 Para ADO 2.7 y versiones anterior, archivo de operaciones de entrada/salida como [abiertos](../../ado/reference/ado-api/open-method-ado-recordset.md) y [guardar](../../ado/reference/ado-api/save-method.md) que se utiliza para leer y escribir en algunos casos, los datos basados en archivos pudieron permitir un nombre de archivo o dirección URL que se usará que especifican un disco no según el tipo de archivo. Por ejemplo, LPT1, COM2, PRN. TXT, AUX podría utilizarse como alias de entrada/salida entre dispositivos e impresoras auxiliares en el sistema con determinadas

 Para ADO 2,8 y versiones posteriores, esta funcionalidad se ha actualizado. Para abrir y guardar **Recordset** y **flujo** objetos, ADO ahora realiza una comprobación de tipo de archivo para asegurarse de que el dispositivo de entrada o salido especificado en un nombre de archivo o dirección URL es un archivo real.

> [!NOTE]
>  Comprobación de tipos de archivo como se describe en esta sección solo se aplica para Windows 2000 y versiones posteriores. No se aplica a las situaciones donde se está ejecutando ADO 2.8 o versiones posterior en las versiones anteriores de Windows, como Windows 98.

