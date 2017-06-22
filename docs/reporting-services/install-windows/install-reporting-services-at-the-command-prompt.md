---
title: "Instalar Reporting Services en el símbolo del sistema | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command line
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f2c8586ba26169bdd236f825b9f9688106788fff
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="install-reporting-services-at-the-command-prompt"></a>Instalación de Reporting Services desde el símbolo del sistema

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite una instalación de línea de comandos desde el programa de instalación de SQL Server. Este tema contiene varios ejemplos de instalaciones desde la línea de comandos que son específicas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener una descripción completa de las opciones de línea de comandos disponibles para todos los componentes de SQL Server, vea [Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). En este tema no se describen las opciones de línea de comandos del complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint. Para obtener información sobre la instalación de comandos del complemento, vea [Instalar el complemento mediante el archivo de instalación rsSharePoint.msi](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint).

##  <a name="bkmk_native_mode"></a> Reporting Services en modo nativo

### <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (modo nativo)
 El valor de entrada primario para instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es el valor de entrada **/RSINSTALLMODE** . El valor tiene dos opciones: **SharePointFilesOnlyMode** y **FilesOnlyMode**  
  
 Si la instalación incluye el motor de base de datos de SQL Server, el modo predeterminado RSINSTALLMODE es DefaultNativeMode. Si la instalación no incluye el motor de base de datos de SQL Server, el modo predeterminado RSINSTALLMODE es FilesOnlyMode. Si elige DefaultNativeMode pero la instalación no incluye el motor de base de datos de SQL Server, la instalación cambia automáticamente RSINSTALLMODE a FilesOnlyMode. Para obtener más información sobre los valores de entrada, vea [Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

### <a name="examples-of-native-mode-installation"></a>Ejemplos de instalación en modo nativo

 En el ejemplo que se muestra a continuación se instala lo siguiente y se configuran las cuentas para:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo.  
  
-   El objeto [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   El Agente SQL Server, que es necesario para las características de suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
```  
Setup.exe /q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /ERRORREPORTING=1 /UPDATEENABLED="False" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Adv_SSMS,RS" /RSINSTALLMODE="DefaultNativeMode" /SQLSVCACCOUNT="[DOMAIN\ACCOUNT]" /SQLSVCPASSWORD="[PASSWORD]" /AGTSVCACCOUNT="[DOMAIN\ACCOUNT]" /AGTSVCPASSWORD="[PASSWORD]" /SQLSYSADMINACCOUNTS="[DOMAIN\ACCOUNT]"  
```  
  
##  <a name="bkmk_sharepoint_mode"></a> modo SharePoint, Reporting Services  
  
### <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (modo de SharePoint)  
 El valor de entrada para instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint es **/RSSHPINSTALLMODE**. El valor de entrada tiene una opción: SharePointFilesOnlyMode. Esta opción instala todos los archivos necesarios para el modo de SharePoint, pero se necesita cierta configuración después de la instalación. Los pasos de configuración adicionales se completan con Administración central de SharePoint. Para obtener más información, vea [Instalación del primer servidor de informes en modo de SharePoint](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).  
  
### <a name="examples-of-sharepoint-mode-installation"></a>Ejemplos de instalación en modo de SharePoint  
 En el ejemplo siguiente se instala el servicio del motor de base de datos de SQL Server y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint junto con el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint (RS_SHPWFE).  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 En el siguiente ejemplo se instala solo el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="[PASSWORD]" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
### <a name="examples-of-sharepoint-mode-upgrade"></a>Ejemplos de actualización en modo de SharePoint  
 Las siguientes actualizaciones de ejemplo del modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . **RSUPGRADEPASSWORD** es la contraseña de la cuenta de servicio del servidor de informes existente. RSUPGRADEPASSWORD es un campo necesario en un escenario de actualización a menos que la cuenta de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sea una cuenta integrada.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="[PASSWORD]"  
```  
  
 El ejemplo siguiente se puede usar para actualizar una instalación en modo de SharePoint basada en la arquitectura de servicio compartido de SharePoint. En el siguiente ejemplo se usa el modificador ALLOWUPGRADEFORSSRSSHAREPOINTMODE. El modificador no es necesario para actualizar versiones anteriores que no se basan en la arquitectura de servicio compartido:  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```

## <a name="next-steps"></a>Pasos siguientes

[Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
[Parámetros de SysPrep](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md#SysPrep)   
[Instalar PowerPivot desde el símbolo del sistema](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
