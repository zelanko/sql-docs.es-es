---
title: Cómo instalar extensiones de seguridad personalizadas | Microsoft Docs
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 103d852f27f2f70f598a4bf1d09bb59fcdbcb8d8
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274903"
---
# <a name="how-to-install-custom-security-extensions"></a>Cómo instalar extensiones de seguridad personalizadas

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 presentó un nuevo portal web para hospedar nuevas API de Odata y además nuevas cargas de trabajo de informes como informes móviles y KPI. Este nuevo portal se basa en tecnologías más recientes y está aislado del conocido servicio Reporting Services, ya que se ejecuta en un proceso independiente. Este proceso no es una aplicación ASP.NET hospedada y, por lo tanto, no admite los supuestos de las extensiones de seguridad personalizadas existentes. Además, las interfaces actuales de las extensiones de seguridad personalizadas no permiten que se pase ningún contexto externo, lo que deja a los implementadores con la única opción de inspeccionar los bien conocidos objetos de ASP.NET globales, lo que exige algunos cambios en la interfaz.

## <a name="what-changed"></a>Cambios

Se presentó una nueva interfaz que puede implementarse y que proporciona un elemento IRSRequestContext que ofrece las propiedades más comunes usadas por las extensiones para tomar decisiones relacionadas con la autenticación.

En versiones anteriores, el Administrador de informes era el front-end y podía configurarse con su propia página de inicio de sesión personalizada. En Reporting Services 2016, solo se admite una página hospedada por reportserver que debe autenticarse en ambas aplicaciones.

## <a name="implementation"></a>Implementación

En versiones anteriores, las extensiones podían basarse en el supuesto común de que los objetos de ASP.NET pronto estarían disponibles. Puesto que el nuevo portal no se ejecuta en ASP.NET, la extensión podría tener problemas con objetos NULL.

El ejemplo más genérico es acceder a HttpContext.Current para leer información de solicitud, como encabezados y cookies. Para permitir que las extensiones tomen las mismas decisiones, se presentó un nuevo método en la extensión que proporciona información de solicitud y se llama al autenticar desde el portal. 

Las extensiones deben implementar la interfaz <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> para aprovecharlo. Las extensiones tienen que implementar ambas versiones del método <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A>, ya que el contexto reportserver y otros usados en el proceso webhost lo llaman. El ejemplo siguiente muestra una de las implementaciones sencillas del portal donde se usa la identidad resuelta por reportserver.

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>Implementación y configuración

Las configuraciones básicas necesarias para la extensión de seguridad personalizada son las mismas que en versiones anteriores. Es necesario realizar cambios en web.config y rsreportserver.config: para más información, vea [Configurar la autenticación de formularios o personalizada en el servidor de informes](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).

Ya no es hay un archivo web.config independiente para el Administrador de informes, sino que el portal hereda la misma configuración que el punto de conexión reportserver.

## <a name="machine-keys"></a>Claves de equipo

En el caso de la autenticación mediante formularios, que exige el descifrado de la cookie de autenticación, ambos procesos deben configurarse con los mismos algoritmo de descifrado y clave de equipo. Este era un paso familiar para aquellos que previamente habían configurado Reporting Services para funcionar en entornos de escalado, pero ahora es un requisito incluso para las implementaciones en un solo equipo.

Debe usar una clave de validación específica para la implementación. Hay varias herramientas para generar las claves, como el Administrador de Internet Information Services (IIS). Puede encontrar otras herramientas pueden en Internet.

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 y posterior

**\ReportServer\rsReportServer.config**

Agregue en `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

Agregue en `<system.web>`.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

Agregue en `<configuration>`.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Servidor de informes de Power BI

Está disponible a partir de la versión de junio de 2017 (compilación 14.0.600.301).

**\ReportServer\rsReportServer.config**

Agregue en `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>Configurar las cookies de acceso directo

El nuevo portal y reportserver se comunican mediante las API internas de Soap para algunas de sus operaciones (como la versión anterior del Administrador de informes). Cuando hay que pasar cookies adicionales desde el portal al servidor, las propiedades PassThroughCookies siguen estando disponibles. Para más información, vea [Configurar el portal web para pasar cookies de autenticación personalizadas](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>Pasos siguientes

[Configuración de la autenticación de formularios o personalizada en el servidor de informes](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Configurar el Administrador de informes para pasar cookies de autenticación personalizadas](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
