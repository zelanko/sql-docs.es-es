---
title: "Configurar la autenticación de formularios o personalizada en el servidor de informes | Documentos de Microsoft"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 325b7d6f1015b6e5e81565df37d1c02d20e5802f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>Configurar la autenticación de formularios o personalizada en el servidor de informes

Reporting Services proporciona una arquitectura extensible que permite conectar módulos de autenticación personalizados o basados en formularios. Podría considerar implementar una extensión de autenticación personalizada si los requisitos de implementación no incluyen la seguridad integrada de Windows o la autenticación básica. El escenario más común para utilizar la autenticación personalizada es admitir el acceso a una extranet o a Internet en una aplicación web. Reemplazar la extensión de autenticación de Windows predeterminada con una extensión de autenticación personalizada le proporciona más control sobre cómo se concede acceso a los usuarios externos al servidor de informes.  

En la práctica, implementar una extensión de autenticación personalizada requiere varios pasos que incluyen copiar los archivos de aplicación y ensamblados, modificar los archivos de configuración y realizar pruebas. Este tema se centra simplemente en la configuración de autenticación que se especifica en los archivos de configuración.  

> [!NOTE]
>  La creación de una extensión de autenticación personalizada requiere código personalizado y conocimientos sobre la seguridad de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Si no desea crear una extensión de autenticación personalizada, puede utilizar grupos y cuentas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory, pero tendrá que reducir en gran parte el ámbito de implementación de un servidor de informes. Para obtener más información sobre la autenticación personalizada, vea [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).

Además, si desea utilizar una extensión de autenticación personalizada o autenticación de formularios en un entorno de SQL Server Reporting Services que está integrado con un producto de SharePoint, debe configurar el sitio de SharePoint para utilizar el método de autenticación que elija. Para obtener más información sobre cómo configurar la autenticación en SharePoint, vea [Ejemplos de autenticación](http://go.microsoft.com/fwlink/?LinkId=115575) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).



### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>Para configurar un servidor de informes de modo que use la autenticación personalizada

1.  Abra RSReportServer.config en un editor de texto.

2.  Buscar \< **autenticación**>.

3.  Copie la estructura XML siguiente:

    ```
    <Authentication>
          <AuthenticationTypes>
                 <Custom />
          </AuthenticationTypes>
          <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    ```

4.  Péguela sobre las entradas existentes para \< **autenticación**>.

     Observe que no puede utilizar **Custom** con otros tipos de autenticación.

5.  Guarde el archivo.

6.  Abra el archivo Web.config para el servidor de informes. De forma predeterminada, se encuentra en la carpeta \Archivos de programa\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer.

7.  Busque **authentication mode** y establézcalo en **Forms**.

    ```
    <authentication mode = "Forms" />
    ```

8.  Busque **identity impersonate** y establézcalo en **False**.

    ```
    <identity impersonate = "false" />  
    ```
9. Agregue la estructura del elemento **PassThroughCookies** al archivo de configuración. Para obtener más información, vea [configurar el Portal Web para pasar Cookies de autenticación personalizada](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
10. Guarde el archivo.  
  
11. Si configuró una implementación escalada, repita todos los pasos anteriores con los demás servidores de informes de la implementación.  
  
12. Reinicie el servidor de informes para borrar las sesiones que estén abiertas en ese momento.  

## <a name="see-also"></a>Vea también

[Implementar una extensión de seguridad](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
[Ejemplo de seguridad personalizada de Reporting Services (GitHub)](https://github.com/Microsoft/Reporting-Services/tree/master/CustomSecuritySample)  
[Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)   
[El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Configurar la autenticación básica en el servidor de informes](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
[Configurar la autenticación de Windows en el servidor de informes](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
¿Más preguntas? [Pruebe el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
