---
title: "Cómo instalar extensiones de seguridad personalizadas | Documentos de Microsoft"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: 3
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e7058e9c0edce2b457dc63bf9e2d5cf61b6ee64f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="how-to-install-custom-security-extensions"></a>Cómo instalar extensiones de seguridad personalizadas
Reporting Services 2016 introdujo un nuevo portal web para hospedar nuevos APIs Odata y también hospedan nuevas cargas de trabajo de informes, como informes móviles y KPI. Este nuevo portal se basa en tecnologías más recientes y está aislada de la ReportingServicesService familiar mediante la ejecución en un proceso independiente. Este proceso no es una aplicación ASP.NET hospedada y por lo tanto interrumpe suposiciones de extensiones de seguridad personalizadas existentes. Además, no permiten las interfaces actuales para extensiones de seguridad personalizadas para que algún contexto externo se pasa, dejando los implementadores con la única opción para inspeccionar los objetos conocidos de ASP.NET global, esto requiere algunos cambios en la interfaz.

## <a name="what-changed"></a>¿Qué cambió?

Se introdujo una nueva interfaz que puede implementarse que proporciona un IRSRequestContext proporciona las propiedades más comunes utilizadas por las extensiones para tomar decisiones relacionadas con la autenticación.
    
En versiones anteriores, el Administrador de informes fue el front-end y puede configurarse con su propia página de inicio de sesión personalizada. En Reporting Services 2016, solo una página hospedada en reportserver es compatible y debe autenticarse en ambas aplicaciones.

## <a name="implementation"></a>Implementación
En versiones anteriores, las extensiones podían confiar en un supuesto común que ASP.NET objetos sería estén disponibles. Puesto que el nuevo portal no se ejecuta en ASP.NET, la extensión podría alcanzó problemas con objetos que se va a NULL.
    
El ejemplo más genérico tiene acceso a HttpContext.Current para leer la información de solicitud, como encabezados y las cookies. Para permitir que las extensiones tomar las mismas decisiones se introdujo un nuevo método en la extensión que proporciona información de la solicitud y se llama al autenticar desde el portal. 
    
Las extensiones deben implementar la <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> interfaz para poder aprovechar esto. Las extensiones necesitará implementar ambas versiones de <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> método, tal y como se llama por el contexto de servidor de informes y otros utilizados en el proceso de webhost. El ejemplo siguiente muestra una de las implementaciones simples para el portal donde la identidad resuelto por el servidor de informes es la utiliza.

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
Las configuraciones básicas necesarias para la extensión de seguridad personalizada son los mismos que las versiones anteriores. Es necesario realizar cambios de web.config y rsreportserver.config: para obtener más información, consulte [configurar personalizado o autenticación de formularios en el servidor de informes](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).
    
Ya no es un archivo web.config independiente para el Administrador de informes, el portal heredará la misma configuración que el punto de conexión del servidor de informes.

## <a name="machine-keys"></a>Claves de equipo

En el caso de autenticación de formularios que requiere el descifrado de la cookie de autenticación, ambos procesos deben configurarse con el mismo algoritmo de clave y el descifrado de máquina. Esto era un paso familiar para aquellos que previamente tenía el programa de instalación Reporting Services para funcionar en entornos de escalado horizontal, pero ahora es un requisito incluso para las implementaciones en un solo equipo.

Por ejemplo:
    
**\ReportServer\web.config**

Agregue bajo `<system.web>`.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.Webhost.exe.config**

Agregue bajo `<configuration>`.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

Debe usar un determinado de clave de validación para la implementación, hay varias herramientas para generar las claves como Internet Information Services Manager (IIS). Otras herramientas pueden encontrarse en internet.

## <a name="configure-passthrough-cookies"></a>Configurar las cookies de paso a través

El nuevo portal y el servidor de informes se comunican mediante las API de soap interno para algunos de sus operaciones (similares a la versión anterior del Administrador de informes). Cuando las cookies adicionales deben pasarse desde el portal en el servidor de las propiedades de PassThroughCookies sigue estando disponible. Para obtener más información, consulte [configurar el Portal Web para pasar Cookies de autenticación personalizada](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="see-also"></a>Vea también

[Configurar la autenticación de formularios o personalizada en el servidor de informes](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Configurar el Administrador de informes para pasar Cookies de autenticación personalizada](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)
