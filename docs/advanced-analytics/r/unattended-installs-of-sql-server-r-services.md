---
title: "Instalación desatendida de servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: babb74aa866404853cfef83e1d30159354f385e7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>Instalación desatendida de servicios de aprendizaje de máquina (In-Database)

En este tema se describe cómo usar argumentos de línea de comandos con el programa de instalación de SQL Server para instalar el aprendizaje automático en una instancia del motor de base de datos, de modo silencioso. En una instalación desatendida, no use las características interactivas de Asistente para la instalación y debe proporcionar todos los argumentos necesarios para completar la instalación, incluidas las licencias de contratos para SQL Server y los componentes de aprendizaje de máquina.

**Se aplica a:** (en bases de datos) de servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

> [!IMPORTANT]
> 
> En SQL Server 2016 y SQL Server 2017, son necesarios pasos adicionales después de que finalice el programa de instalación para habilitar la característica. Éstos incluyen una reconfiguración y reiniciaron la instancia. No olvide revisar todos los pasos.

## <a name="prerequisites"></a>Requisitos previos

+ Debe instalar el motor de base de datos en cada instancia donde va a usar aprendizaje automático.

+ Si el equipo no tiene acceso a Internet, asegúrese de instalar a los instaladores para los componentes de aprendizaje con antelación automático. Para ubicaciones de descarga, vea [instalación de componentes de aprendizaje de máquina sin acceso a Internet](../../advanced-analytics/r/installing-ml-components-without-internet-access.md).

+ Hay nuevas licencias parámetros relacionados con los componentes de código abierto de R y Python. Debe aceptar los términos de licencia con un argumento independiente para cada idioma instalado. Si no incluye este parámetro en la línea de comandos, se producirá un error en la instalación.

+ Para completar el programa de instalación sin tener que responder a las solicitudes, asegúrese de que se han identificado todos los argumentos necesarios, los de licencia y para las demás características que desea instalar incluidos.

> [!NOTE] 
> Se requiere el modo de seguridad mixto que es compatible con los inicios de sesión SQL en las primeras versiones. Sin embargo, puede habilitar la autenticación de modo mixto admitir el desarrollo de soluciones científicos de datos mediante un inicio de sesión SQL.

## <a name="bkmk_NewInstall"></a>Instalación desatendida de servicios de aprendizaje de máquina con R

El siguiente ejemplo se muestra la **mínimo** instalan características necesarias para especificar la línea de comandos al realizar un silenciosa, desatendida de servicios de máquinas de 2017 (In-Database) de SQL Server.

1. Abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    
    Tenga en cuenta las marcas necesarias para R en SQL Server 2017: `ADVANCEDANALYTICS`, `SQL_INST_MR`, y `IACCEPTROPENLICENSETERMS`.
2. Reinicie el servidor.
3. Realice los pasos de configuración posteriores a la instalación como se describe en [en esta sección](#bkmk_PostInstall). Se deberán volver a reiniciar los servicios de SQL Server.

## <a name="OldInstall"></a>Instalación desatendida de R Services (In-Database)
 
 El siguiente ejemplo se muestra la **mínimo** instalan características necesarias para especificar la línea de comandos al realizar un silenciosa, desatendida de servicios de SQL Server 2016 R.

1. Abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    Tenga en cuenta las marcas necesarias para los servicios de R de 2016: `ADVANCEDANALYTICS` y `IACCEPTROPENLICENSETERMS`.
2. Reinicie el servidor.
3. Realice los pasos de configuración posteriores a la instalación como se describe en [en esta sección](#bkmk_PostInstall). Se deberán volver a reiniciar los servicios de SQL Server.

## <a name = "bkmk_PostInstall"></a>Pasos adicionales después de la instalación

1.  Una vez completada la instalación, abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y ejecute el siguiente comando para habilitar la característica.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Debe habilitar explícitamente la característica y volver a configurar; en caso contrario, no será posible invocar los scripts externos incluso si se ha instalado la característica.
  
2.  Reinicie el servicio de SQL Server para la instancia ha vuelto a configurar. Si lo hace, se reiniciará automáticamente relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] también el servicio.

3. Es posible que se requieran pasos adicionales si tiene una configuración de seguridad personalizada o si va a usar SQL Server para admitir contextos de cálculo remotos. Para más información, vea [Preguntas más frecuentes sobre actualización e instalación (SQL Server)](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md).

