---
title: Configurar el correo electrónico para una aplicación de servicio de Reporting Services (SharePoint 2010 y SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6caa06af68eddfd85cb4f19ab2cfb8dd41bbdd95
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798110"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application-sharepoint-2010-and-sharepoint-2013"></a>Configurar el correo electrónico para una aplicación de servicio de Reporting Services (SharePoint 2010 y SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la alerta de datos envía las alertas en mensajes de correo electrónico. Para enviar correo electrónico, quizás tenga que configurar la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y modificar la extensión de entrega de correo electrónico para ella. También se requiere la configuración del correo electrónico si piensa utilizar la extensión de entrega por correo electrónico para la característica de suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint &#124; SharePoint 2010 y SharePoint 2013.|  
  
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
  
1.  Si el entorno de correo electrónico requiere la autenticación NTLM y no permite el acceso anónimo, necesita modificar la configuración de la extensión de entrega por correo electrónico para las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Cambie **smtpauthenticate** para que use un valor de "2". Este valor no se puede cambiar desde la interfaz de usuario. En el ejemplo de script de PowerShell siguiente se actualiza la configuración completa de la extensión de entrega por correo electrónico del servidor de informes para la aplicación de servicio denominada "SSRS_TESTAPPLICATION". Tenga en cuenta que algunos de los nodos enumerados en el script también se pueden establecer desde la interfaz de usuario, por ejemplo la dirección "De".  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml
    $emailXml = [xml]$emailCfg
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  Si necesita comprobar el nombre de la aplicación de servicio, ejecute el cmdlet **Get-SPRSServiceApplication** .  
  
    ```powershell
    Get-SPRSServiceApplication  
    ```  
  
3.  En el ejemplo siguiente se devolverán los valores actuales de la extensión de correo electrónico para la aplicación de servicio denominada "SSRS_TESTAPPLICATION".  
  
    ```powershell
    $app = get-sprsserviceapplication | Where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
    ```  
  
4.  En el ejemplo siguiente se creará un archivo denominado "emailconfig.txt" con los valores actuales de la extensión de correo electrónico para la aplicación de servicio denominada "SSRS_TESTAPPLICATION".  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | Select -ExpandProperty ConfigurationXml | Out-File c:\emailconfig.txt  
    ```
