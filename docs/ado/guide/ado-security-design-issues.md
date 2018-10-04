---
title: Problemas de diseño de seguridad de ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c961c24f0ffcbb3f0cbafabce2988edb6c8d607
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716373"
---
# <a name="ado-security-design-features"></a>Características de diseño de seguridad de ADO
Las secciones siguientes describen las características de diseño de seguridad de ActiveX Data Objects (ADO) 2.8 y versiones posteriores. Estos cambios se realizaron en ADO 2.8 para mejorar la seguridad. ADO 6.0, que se incluye en Windows DAC 6.0 en Windows Vista, es funcionalmente equivalente a ADO 2.8, que se incluyó en MDAC 2.8 en Windows XP y Windows Server 2003. En este tema se proporciona información sobre cómo proteger mejor sus aplicaciones en ADO 2.8 o posterior.

> [!IMPORTANT]
>  Si va a actualizar la aplicación desde una versión anterior de ADO, se recomienda probar la aplicación actualizada en un equipo que no sea de producción antes de implementarla para los clientes. De este modo, puede asegurarse de que es conscientes de los problemas de compatibilidad antes de implementar la aplicación actualizada.

## <a name="internet-explorer-file-access-scenarios"></a>Escenarios de acceso de archivo de Internet Explorer
 El efecto de las características siguientes el funcionamiento de ADO a 2.8 y versiones posterior cuando se utiliza en las páginas Web en Internet Explorer de la secuencia de comandos.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Cuadro de mensaje de advertencia de seguridad mejorado y revisado usa ahora para avisar a los usuarios
 Para ADO 2.7 y versiones anterior, el siguiente mensaje de advertencia aparece cuando se trata de una página Web con script ejecutar código ADO de un proveedor de confianza:

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Para ADO 2.8 y versiones posterior, ya no aparece el mensaje anterior. En su lugar, aparece el siguiente mensaje en este contexto:

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 El mensaje anterior permite al usuario tomar una decisión informada, sabiendo las consecuencias para cualquiera de las opciones:

-   Si el usuario confía en el sitio, haga clic en Aceptar permitirá todo el código con seguridad de disco (todos los métodos de ADO y propiedades con las excepciones de las API accesibles para el disco se describe más adelante en este tema) para ejecutar y se ejecutan en la ventana del explorador.

-   Si el usuario no confía en el sitio, haga clic en Cancelar bloquea el código de ADO para el acceso a datos desde la ejecución y ejecutar en su totalidad.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Código accesible para el disco limitado ahora a sitios de confianza
 Se realizaron cambios de diseño adicionales en ADO 2.8 que restringir específicamente la capacidad de un conjunto limitado de API, lo cual podrían exponer la posibilidad de leer o escribir en archivos en el equipo local. Estos son los métodos de API que han sido más restringido por motivos de seguridad cuando se ejecuta Internet Explorer:

-   Para la propiedad ADO **Stream** objeto, si la [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) o [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) se usan los métodos.

-   Para ADO **Recordset** objeto, si bien la [guardar](../../ado/reference/ado-api/save-method.md) método o la [abierto](../../ado/reference/ado-api/open-method-ado-recordset.md) método, por ejemplo, cuando cualquier el **adCmdFile** opción está establecida o el [proveedor Microsoft OLE DB persistencia (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) se utiliza.

 Estos conjuntos de limitado de funciones disco potencialmente accesibles, ocurre lo siguiente para ADO 2.8 y versiones posterior, si se ejecuta cualquier código que utilice estos métodos en Internet Explorer:

-   Si el sitio que proporciona el código se ha agregado anteriormente a la lista de la zona de sitios de confianza, el código se ejecuta en el explorador y se concede acceso a archivos locales.

-   Si el sitio no aparece en la lista de la zona de sitios de confianza, el código está bloqueado y se deniega el acceso a archivos locales.

    > [!NOTE]
    >  En ADO 2.8 y versiones posterior, el usuario no es una alerta o recomienda agregar sitios a la lista de la zona de sitios de confianza. Por lo tanto, la administración de la lista de sitios de confianza es responsabilidad de aquellos que se va a implementar o que admiten aplicaciones basadas en sitio Web que requieren acceso al sistema de archivos local.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Acceso bloqueado a la propiedad ActiveCommand en objetos de conjunto de registros
 Cuando se ejecuta en Internet Explorer, ADO 2.8 ahora bloquea el acceso a la [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) propiedad para un activo **Recordset** de objetos y devuelve un error. El error se produce independientemente de si la página procede de un sitio Web que se registra en la lista de sitios de confianza.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Cambios en el control para proveedores OLE DB y la seguridad integrada
 Mientras revisa ADO 2.7 y versiones anteriores de los posibles problemas de seguridad y problemas, se detectó el siguiente escenario:

 En algunos casos, los proveedores OLE DB que admiten la seguridad integrada [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) propiedad potencialmente podría permitir que las páginas Web con script para volver a usar el objeto de conexión de ADO para conectarse de forma no intencionada a otros servidores con las credenciales de inicio de sesión actual de los usuarios. Para evitar esto, ADO 2.8 y versiones posterior controlan los proveedores de OLE DB, dependiendo de cómo ha elegido para proporcionar o no se proporciona, para la seguridad integrada.

 Para las páginas Web que se cargan desde sitios que se indican en la lista de la zona de sitios de confianza, en la tabla siguiente proporciona un desglose de cómo ADO 2.8 y versiones posterior administra las conexiones de ADO en cada caso.

|Configuración de Internet Explorer para la autenticación de usuario, de inicio de sesión|Admite el proveedor "Integrated Security" y UID y PWD están especificados (SQLOLEDB)|Proveedor no admite "Integrated Security" (MSPersist JOLT, MSDASQL)|Proveedor es compatible con "Integrated Security" y se establece en SSPI (no se especifica ningún UID y PWD)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Inicio de sesión automático con el nombre de usuario actual y la contraseña|Permitir la conexión|Permitir la conexión|Permitir la conexión|
|Símbolo del sistema para el nombre de usuario y contraseña|Permitir la conexión|Un error de conexión|Un error de conexión|
|Inicio de sesión automático solo en la zona de Intranet|Permitir la conexión|Preguntar al usuario con una advertencia de seguridad|Preguntar al usuario con una advertencia de seguridad|
|Inicio de sesión anónimo|Permitir la conexión|Un error de conexión|Un error de conexión|

 En el caso donde aparece la advertencia de seguridad ahora, el cuadro de mensaje informa a los usuarios:

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 El mensaje anterior permite al usuario tomar una decisión más informada y actúe en consecuencia.

> [!NOTE]
>  Para sitios de confianza (es decir, los sitios no aparecen en la lista de la zona de sitios de confianza), si el proveedor también es de confianza (como se ha descrito anteriormente en esta sección), el usuario podría ver dos advertencias de seguridad en una fila, una advertencia sobre el proveedor no seguro y una segunda advertencia la intento de utilizar su identidad. Si el usuario hace clic en Aceptar para la primera advertencia, se ejecutan la configuración de Internet Explorer y el código de respuesta comportamiento descrito en la tabla anterior.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Controlar si el texto de la contraseña se devuelve en las cadenas de conexión de ADO
 Al intentar obtener el valor de la [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad ADO **conexión** objeto, se producen los eventos siguientes:

1.  Si la conexión está abierta, se realiza, a continuación, una llamada de inicialización para el proveedor OLE DB subyacente para obtener la cadena de conexión.

2.  Dependiendo de la configuración en el proveedor OLE DB de la [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) propiedad, las contraseñas se incluye junto con otra información de la cadena de conexión que se devuelve.

 Por ejemplo, si la propiedad dinámica de conexión ADO **Persist Security Info** está establecido en **True**, se incluye información de contraseña en la cadena de conexión devuelta. En caso contrario, si el proveedor subyacente ha establecido la propiedad **False** (por ejemplo, con el proveedor SQLOLEDB), se omite la información de contraseña en la cadena de conexión devuelta.

 Si usa aplicaciones de terceros (es decir, que no sean de Microsoft) proveedores OLE DB con el código de aplicación ADO, podría comprobar cómo el **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** se implementa la propiedad para determinar si la inclusión de se permite la información de contraseña con cadenas de conexión de ADO.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Comprobación de los dispositivos no es un archivo al cargar y guardar los conjuntos de registros o secuencias
 Para ADO 2.7 y versiones anterior, archivo operaciones de entrada/salida, como [abierto](../../ado/reference/ado-api/open-method-ado-recordset.md) y [guardar](../../ado/reference/ado-api/save-method.md) que se usaron para leer y escribir en algunos casos, los datos basados en archivos podrían permitir un nombre de archivo o dirección URL que se usará que especifican un disco no según el tipo de archivo. Por ejemplo, LPT1, COM2, PRN. TXT, AUX podría utilizarse como alias de entrada/salida, entre las impresoras auxiliares dispositivos y en el sistema con determinados

 Para ADO 2.8 y versiones posterior, esta funcionalidad se ha actualizado. Para abrir y guardar **Recordset** y **Stream** los objetos ADO ahora realiza una comprobación de tipo de archivo para asegurarse de que el dispositivo de entrada o salido especificado en un dirección URL o nombre de archivo es un archivo real.

> [!NOTE]
>  Comprobación de tipos de archivo como se describe en esta sección solo se aplica para Windows 2000 y versiones posteriores. No se aplica a las situaciones donde se está ejecutando en versiones anteriores de Windows, como Windows 98 ADO 2.8 o posterior.
