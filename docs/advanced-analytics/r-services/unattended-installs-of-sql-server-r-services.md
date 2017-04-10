---
title: "Instalaciones desatendidas de servicios SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 14
---
# Instalaciones desatendidas de servicios SQL Server R
    
Antes de comenzar el proceso de instalación, tenga en cuenta estos requisitos:

+ Debe instalar el motor de base de datos en cada instancia que use servicios de R (en bases de datos) en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
+ Si está realizando una instalación sin conexión, debe descargar los componentes necesarios de R de antemano y copiarlos en una carpeta local. Ubicaciones de descarga, consulte [instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).   
+ Hay un nuevo parámetro */IACCEPTROPENLICENSETERMS*, que indica que ha aceptado los términos de licencia para el uso de los componentes de R abierto. Si no incluye este parámetro en la línea de comandos, se producirá un error en el programa de instalación.  
  
## Realización de una instalación desatendida de R Services (en bases de datos)  
 En el ejemplo siguiente se muestran las características mínimas necesarias para especificar la línea de comandos al realizar una instalación silenciosa y desatendida de R Services en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
###  <a name="bkmk_Unattended"></a>  
  
1.  Ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
  
2.  Después de completar la instalación, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute el siguiente comando para habilitar la característica.  
  
    ```  
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with  override  
  
    ```  
  
    > [!NOTE]  
    >  Debe habilitar explícitamente la característica del motor; de otro modo, no será posible invocar los scripts de R incluso si la característica se ha instalado por la configuración.  
  
3.  Reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto también reiniciará automáticamente el servicio relacionado de [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .  
  
## Vea también  
 [Solución de problemas con el programa de instalación R Services](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  