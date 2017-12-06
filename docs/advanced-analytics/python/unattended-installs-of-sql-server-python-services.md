---
title: "Instalación desatendida de servicios de aprendizaje de máquina de Python (In-Database) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77d9a8fcaca2aa8161d6763cda74239754da41d5
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="unattended-installation-of-python-machine-learning-services-in-database"></a>Instalación desatendida de servicios de aprendizaje de máquina de Python (In-Database)

En este tema se describe cómo utilizar los argumentos de línea de comandos en el programa de instalación de SQL Server 2017 para instalar el motor de base de datos de SQL Server con servicios de aprendizaje de máquina y Python, utilizando el modo silencioso.

> [!NOTE]
> No olvide incluir los argumentos de línea de comandos para los contratos de licencia, uno para Python y otro para SQL Server.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar el proceso de instalación, tenga en cuenta estos requisitos:

+ No se puede instalar el servicio de Python independientemente el motor de base de datos de SQL Server 2017. Debe incluir la característica del motor de base de datos SQL.
+ Si está realizando una instalación sin conexión, debe descargar los componentes necesarios de Python de antemano y cópielos en una carpeta local. Para ubicaciones de descarga, vea [instalar componentes de aprendizaje de máquina sin acceso a Internet](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).
+ Hay un nuevo parámetro, */IACCEPTPYTHONLICENSETERMS*, que indica que se han aceptado los términos de licencia para el uso de los componentes de Python proporcionados por Continuum Analytics. Si no incluye este parámetro en la línea de comandos, se producirá un error en la instalación.
+ Para completar el programa de instalación sin tener que responder a las solicitudes, asegúrese de que se han identificado todos los argumentos necesarios, los de Python y licencias de SQL Server y para las demás características que desea instalar incluidos.
+  Se requiere autenticación de modo mixto en algunas versiones preliminares de SQL Server 2016. Ya no es necesario, aunque puede ser útil en escenarios donde los científicos de datos son desarrollar y probar soluciones de forma remota con los inicios de sesión SQL.

## <a name="perform-an-unattended-installation-of-python-machine-learning-services-in-database"></a>Realizar una instalación desatendida de servicios de aprendizaje de máquina de Python (In-Database)

El siguiente ejemplo se muestra la **mínimo** requiere características para especificar la línea de comandos al realizar una instalación silenciosa y desatendida de Python y el motor de base de datos en la instancia predeterminada.

> [!NOTE]
> Esta característica requiere que SQL Server 2017. Python no se admite en versiones anteriores de SQL Server.

1. Abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONLICENSETERMS
    ```

    > [!NOTE]
    > 
    > Hay marcas nuevo el programa de instalación para Python: `SQL_INST_MPY` y`IACCEPTPYTHONLICENSETERMS`

2. Reinicie el servidor como se indica.
3. Realice los pasos de configuración posteriores a la instalación como se describe en [en esta sección](#bkmk_PostInstall). Se deberán volver a reiniciar los servicios de SQL Server.

## <a name = "bkmk_PostInstall"></a>Pasos posteriores a la instalación

1.  Una vez completada la instalación, abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y ejecute el siguiente comando para habilitar la característica.

    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Debe habilitar explícitamente la característica y volver a configurar; en caso contrario, no será posible invocar los scripts externos incluso si se ha instalado la característica.
  
3.  Reinicie el servicio de SQL Server para la instancia ha vuelto a configurar. Si lo hace, se reiniciará automáticamente relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] también el servicio.

3. Es posible que se requieran pasos adicionales si tiene una configuración de seguridad personalizada o si va a usar SQL Server para admitir contextos de cálculo remotos. Para obtener más información, consulte [solucionar problemas de instalación de aprendizaje de máquina](../machine-learning-troubleshooting-faq.md).
