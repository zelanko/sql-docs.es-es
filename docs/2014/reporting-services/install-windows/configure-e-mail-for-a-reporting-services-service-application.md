---
title: Configurar el correo electrónico para la aplicación de servicio (SharePoint 2010 y SharePoint 2013) de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5432b0d2fa1c5fd7504b4706fb85b240efeb9c34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236225"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application-sharepoint-2010-and-sharepoint-2013"></a>Configurar el correo electrónico para una aplicación de servicio de Reporting Services (SharePoint 2010 y SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la alerta de datos envía las alertas en mensajes de correo electrónico. Para enviar correo electrónico, quizás tenga que configurar la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y modificar la extensión de entrega de correo electrónico para ella. También se requiere la configuración del correo electrónico si piensa utilizar la extensión de entrega por correo electrónico para la característica de suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo de SharePoint &#124; SharePoint 2010 y SharePoint 2013.|  
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>Para configurar el correo electrónico para el servicio compartido  
  
1.  En Administración central de SharePoint, haga clic en **Administración de aplicaciones**.  
  
2.  En el grupo **Aplicaciones de servicio** , haga clic en **Administrar aplicaciones de servicio**.  
  
3.  En la lista **Nombre** , haga clic en el nombre de su aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Haga clic en **Configuración de correo electrónico** en la página **Administrar la aplicación de Reporting Services** .  
  
5.  Seleccione **Utilizar servidor SMTP**.  
  
6.  En el cuadro **Servidor SMTP saliente** , escriba el nombre de un servidor SMTP.  
  
7.  En el cuadro **De la dirección** , escriba una dirección de correo electrónico.  
  
     Esta dirección es el remitente de todos los mensajes de correo electrónico alertas.  
  
     La cuenta del usuario especificada en **De la dirección** debe ser una cuenta administrada que especificó cuando configuró el grupo de aplicaciones para la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si tiene permiso, puede ver una lista de las cuentas administradas que existen en la página Cuentas de servicio de Administración central de SharePoint.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>Autenticación NTLM  
  
1.  Si el entorno de correo electrónico requiere la autenticación NTLM y no permite el acceso anónimo, necesita modificar la configuración de la extensión de entrega por correo electrónico para las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Cambie **SMTPAuthenticate** para utilizar el valor "2". Este valor no se puede cambiar desde la interfaz de usuario. El siguiente ejemplo del script de PowerShell actualiza la configuración completa de la extensión de entrega por correo electrónico del servidor de informes para la aplicación de servicio denominada "SSRS_TESTAPPLICATION". Tenga en cuenta que algunos de los nodos enumerados en el script también se pueden establecer desde la interfaz de usuario, por ejemplo la dirección "De".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
    $emailXml = [xml]$emailCfg   
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = “your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = “your FROM email address”  
    Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  Si necesita comprobar el nombre de la aplicación de servicio, ejecute el cmdlet **Get-SPRSServiceApplication**.  
  
    ```  
    get-sprsserviceapplication  
    ```  
  
3.  En el siguiente ejemplo se devolverán los valores actuales de la extensión de correo electrónico para la aplicación de servicio denominada "SSRS_TESTAPPLICATION".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
    ```  
  
4.  El siguiente ejemplo creará un nuevo archivo denominado "emailconfig.txt" con los valores actuales de la extensión de correo electrónico para la aplicación de servicio denominada "SSRS_TESTAPPLICATION".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml | out-file c:\emailconfig.txt  
    ```  
  
  
