---
title: "Instalación desatendida de servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 7d41bd73398c016b920fa67244ffea1af865bde2
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>Instalación desatendida de servicios de aprendizaje de máquina (In-Database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo usar argumentos de línea de comandos con el programa de instalación de SQL Server para instalar los componentes de aprendizaje automático.

Instalación desatendida, se entiende que no utilice las características interactivas de Asistente para la instalación y en su lugar, proporcione todos los argumentos necesarios para completar la instalación, incluidas las licencias de contratos para SQL Server y los componentes de aprendizaje de máquina en un línea de comandos o como parte de una secuencia de comandos, normalmente se encuentra en modo silencioso.

+ [SQL Server 2016 R Services](#bkmk_OldInstall)
+ [Servicios de aprendizaje de máquina SQL Server de 2017](#bkmk_NewInstall) con R o Python
+ [Microsoft R Server o servidor de aprendizaje de máquina](../r/install-microsoft-r-server-from-the-command-line.md)

**Se aplica a: servicios de aprendizaje automático de 2017 SQL Server (en bases de datos), SQL Server 2016 R Services**

## <a name="prerequisites"></a>Requisitos previos

+ Debe instalar el motor de base de datos en cada instancia donde va a usar aprendizaje automático.

+ Si el equipo no tiene acceso a Internet, asegúrese de descargar a los instaladores para los componentes de aprendizaje con antelación automático. Vea [instalación de componentes de aprendizaje de máquina sin acceso a Internet](../r/installing-ml-components-without-internet-access.md).

+ No hay licencias parámetros para cada uno de los componentes de código abierto de R y Python independiente. SQL Server 2016 admite solo R; Es compatible con SQL Server 2017 R y Python. Debe aceptar los términos de licencia para cada idioma instalado. El programa de instalación produce un error si no incluye este parámetro en la línea de comandos.

+ Para completar el programa de instalación sin tener que responder a las solicitudes, asegúrese de que se han identificado todos los argumentos necesarios, los de licencia y para las demás características que desea instalar incluidos.

+ El **Mixed** se requiere el modo de seguridad que es compatible con los inicios de sesión SQL en las primeras versiones. Aunque ya no es necesario, considere la posibilidad de habilitar la autenticación de modo mixto admitir el desarrollo de soluciones científicos de datos que utilice un inicio de sesión SQL.

> [!IMPORTANT]
> 
> Una vez finalizada la instalación para habilitar la característica, se requieren pasos adicionales. Éstos incluyen una reconfiguración y reiniciaron la instancia. Seguro para revisar todos los elementos en la sección [pasos posteriores a la instalación] (#bkmk_PostInstall) para determinar las acciones necesitarse una vez completada la instalación.

## <a name="bkmk_NewInstall"></a>Instalación de línea de comandos para SQL Server 2017

Los siguientes ejemplos incluyen el **mínimo** características necesarias.

> [!IMPORTANT]
> No olvide ejecutar todos los comandos desde un símbolo del sistema con privilegios elevados.
> 
> Una vez completada la instalación, son necesarios algunos pasos adicionales. Vea [en esta sección](#bkmk_PostInstall). 
> Una vez completada la configuración, se requerirán volver a reiniciar los servicios de SQL Server.

### <a name="install-r-only"></a>Instalar R

El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de servicios de máquinas de 2017 (In-Database) de SQL Server con el lenguaje R agregado.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

Tenga en cuenta las marcas necesarias para R en SQL Server 2017:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MR`
+ `IACCEPTROPENLICENSETERMS`.

### <a name="install-python-only"></a>Solo instalar Python

El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de servicios de máquinas de 2017 (In-Database) de SQL Server con el lenguaje de Python agregado.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

Tenga en cuenta las marcas necesarias para Python en SQL Server 2017:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

### <a name="install-both-r-and-python-on-a-named-instance"></a>Instalar R y Python en una instancia con nombre

El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de servicios de máquinas de 2017 (In-Database) de SQL Server en una instancia con nombre. Se agregan los lenguajes R y Python.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

## <a name="OldInstall"></a>Instalación de línea de comandos para SQL Server 2016
 
El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de SQL Server 2016 con el lenguaje R agregado.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

Tenga en cuenta las marcas necesarias para 2016 R Services:

+ `ADVANCEDANALYTICS`
+ `IACCEPTROPENLICENSETERMS`

## <a name = "bkmk_PostInstall"></a>Pasos adicionales después de la instalación

Debe realizar los pasos siguientes una vez completada, independientemente de qué versión instala el programa de instalación de SQL Server. características de aprendizaje de máquina no están habilitadas de forma predeterminada y deben habilitarse explícitamente.

1.  Una vez completada la instalación, abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y ejecute el siguiente comando para habilitar la característica.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Debe habilitar explícitamente la característica y volver a configurar; en caso contrario, no será posible invocar los scripts externos incluso si se ha instalado la característica.
  
2.  Reinicie el servicio de SQL Server para la instancia ha vuelto a configurar. Si lo hace, se reiniciará automáticamente relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] también el servicio.

> [!IMPORTANT]
> 
> Si tiene una configuración de seguridad personalizada, o si va a usar SQL Server como un contexto de proceso al ejecutar código R o Python desde un cliente remoto, pueden ser necesarios algunos pasos adicionales. 
> 
> Para obtener más información, consulte [preguntas más frecuentes de actualización e instalación](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md).
