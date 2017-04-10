---
title: "Configurar la autenticaci&#243;n de formularios o personalizada en el servidor de informes | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Autenticación de formularios, configurar"
  - "autenticación personalizada [Reporting Services]"
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
caps.latest.revision: 20
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Configurar la autenticaci&#243;n de formularios o personalizada en el servidor de informes
  Reporting Services proporciona una arquitectura extensible que permite conectar módulos de autenticación personalizados o basados en formularios. Podría considerar implementar una extensión de autenticación personalizada si los requisitos de implementación no incluyen la seguridad integrada de Windows o la autenticación básica. El escenario más común para utilizar la autenticación personalizada es admitir el acceso a una extranet o a Internet en una aplicación web. Reemplazar la extensión de autenticación de Windows predeterminada con una extensión de autenticación personalizada le proporciona más control sobre cómo se concede acceso a los usuarios externos al servidor de informes.  
  
 En la práctica, implementar una extensión de autenticación personalizada requiere varios pasos que incluyen copiar los archivos de aplicación y ensamblados, modificar los archivos de configuración y realizar pruebas. Este tema se centra simplemente en la configuración de autenticación que se especifica en los archivos de configuración.  
  
> [!NOTE]  
>  La creación de una extensión de autenticación personalizada requiere código personalizado y conocimientos sobre la seguridad de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Si no desea crear una extensión de autenticación personalizada, puede utilizar grupos y cuentas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory, pero tendrá que reducir en gran parte el ámbito de implementación de un servidor de informes. Para obtener más información sobre la autenticación personalizada, vea [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).  
  
 Además, si desea utilizar una extensión de la autenticación personalizada o de la autenticación de formularios en un entorno de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que esté integrado con un producto de SharePoint, debe configurar el sitio de SharePoint para utilizar el método de autenticación que elija. Para obtener más información sobre cómo configurar la autenticación en SharePoint, vea [Ejemplos de autenticación](http://go.microsoft.com/fwlink/?LinkId=115575) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).  
  
### Para configurar un servidor de informes de modo que use la autenticación personalizada  
  
1.  Abra RSReportServer.config en un editor de texto.  
  
2.  Busque \<**Autenticación**>.  
  
3.  Copie la estructura XML siguiente:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <Custom />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
4.  Péguela sobre las entradas existentes para \<**Autenticación**>.  
  
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
  
9. Abra el archivo Web.config del Administrador de informes. De forma predeterminada, se encuentra en la carpeta \Archivos de programa\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportManager.  
  
10. Busque **authentication mode** y establézcalo en **Forms**.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
11. Busque **identity impersonate** y establézcalo en **False**.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
12. Agregue la estructura del elemento **PassThroughCookies** al archivo de configuración. Para obtener más información, vea [Configurar el Administrador de informes para pasar cookies de autenticación personalizada](../Topic/Configure%20Report%20Manager%20to%20Pass%20Custom%20Authentication%20Cookies.md).  
  
13. Guarde el archivo.  
  
14. Si configuró una implementación escalada, repita todos los pasos anteriores con los demás servidores de informes de la implementación.  
  
15. Reinicie el servidor de informes para borrar las sesiones que estén abiertas en ese momento.  
  
## Vea también  
 [Implementar una extensión de seguridad](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
 [Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)   
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Configurar la autenticación básica en el servidor de informes](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
 [Configurar la autenticación de Windows en el servidor de informes](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
  
  