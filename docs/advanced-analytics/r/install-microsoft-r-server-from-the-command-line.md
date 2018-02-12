---
title: "Instalar servidor de aprendizaje de máquina (independiente) o Microsoft R Server (independiente) desde la línea de comandos | Documentos de Microsoft"
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
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 95f8e0c688a2f141ce066e3831e461509d72c1a9
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="install-machine-learning-server-standalone-or-microsoft-r-server-standalone-from-the-command-line"></a>Instalar servidor de aprendizaje de máquina (independiente) o Microsoft R Server (independiente) desde la línea de comandos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe cómo usar argumentos de línea de comandos de SQL Server para instalar las siguientes características de SQL Server mediante la línea de comandos:

+ [Server (independiente) de aprendizaje automático de SQL Server de 2017](#bkmk_mls2017) 
+ [Microsoft R Server (independiente), en SQL Server 2016](#bkmk_mrs2016)

Un **desatendida** instalación requiere que especifique la ubicación de la utilidad de instalación y usan argumentos para indicar las características que desea instalar.

Para efectuar una instalación **silenciosa** , proporcione los mismos argumentos y agregue el conmutador **/q** . No se proporciona ningún mensaje y se requiere ninguna interacción. Sin embargo, el programa de instalación produce un error si se omiten los argumentos necesarios.

## <a name="prerequisites"></a>Requisitos previos

Debe saber cómo realizar una instalación de línea de comandos de SQL Server y estar familiarizado con los argumentos de secuencias de comandos.

Para obtener más información, consulte [instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).

Si instala el servidor de aprendizaje de máquina o Microsoft R Server (independiente) en un equipo que no tenga acceso a Internet, debe descargar los componentes necesarios de R (o Python) de antemano y cópielos en una carpeta local. Para ubicaciones de descarga, vea [instalación de componentes de aprendizaje de máquina sin acceso a internet](installing-ml-components-without-internet-access.md).


## <a name="bkmk_mls2017"></a>Instalar Microsoft Machine Learning Server (independiente)

**Se aplica a: SQL Server de 2017**

Ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados para instalar solo servidor de aprendizaje de máquina (independiente) y sus requisitos previos.

+ Se requiere, el argumento de características que los términos de licencia de SQL Server.
+ Puede instalar un idioma, o tanto R y Python, pero tiene una licencia independiente para cada uno.

Este ejemplo muestra los argumentos usados para instalar R.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Este ejemplo muestra los argumentos usados para instalar Python.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MPY  /IACCEPTPYTHONOPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

+ Para ver el progreso y los mensajes, quite el argumento _/q_.
+ Si utiliza el argumento **características = SQL_SHARED_MR**, se instalan sólo los componentes de servidor de aprendizaje de máquina, con R ni Python. Esta instalación incluye todos los requisitos previos, que se instalan en modo silencioso, de forma predeterminada. Sin embargo, se recomienda que agregue al menos un idioma al instalar por primera vez.
+ Agregar **SQL_INST_MR** para instalar la compatibilidad con R.
+ Agregar **SQL_INST_MPY** para instalar la compatibilidad con Python.
+ **IACCEPTROPENLICENSETERMS** indica que ha aceptado los términos de la licencia para usar los componentes de R de código abierto.
+ **IACCEPTPYTHONLICENSETERMS** indica han aceptado los términos de licencia para el uso de los componentes de Python.
+ **IACCEPTSQLSERVERLICENSETERMS** es obligatorio para ejecutar el Asistente para la instalación.


## <a name="bkmk_mrs2016"></a> Instalar Microsoft R Server (independiente)

**Se aplica a: SQL Server 2016**

Ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados para instalar **sólo** Microsoft R Server (independiente) y sus requisitos previos. 

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

> [!TIP]
> Se recomienda que no instale este en el mismo equipo que hospeda una instancia de SQL Server R Services.

## <a name="post-installation-tasks"></a>Tareas posteriores a la instalación

Para configurar la otra instancia de Microsoft R Server con los mismos parámetros, puede reutilizar el archivo de configuración que se crea durante la instalación. Para obtener más información, consulte [instalar SQL Server con un archivo de configuración](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md).

### <a name="review-installed-components"></a>Componentes de revisión instalada

Una vez concluida la instalación, puede revisar el archivo de configuración creado por el programa de instalación de SQL Server, junto con un resumen de las acciones de instalación.

De forma predeterminada, todo el programa de instalación registros y resúmenes para SQL Server y características relacionadas se crean en las siguientes carpetas:

+ 2017 de SQL Server:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`
+ SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`

Se crea una subcarpeta independiente para cada característica que se ha instalado.

### <a name="customize-the-r-or-python-environment"></a>Personalizar el entorno de R o Python

Después de la instalación, puede instalar paquetes de R o Python adicionales. El proceso varía ligeramente en función de si usas SQL Server 2016 o 2017 de SQL Server.

En SQl Server 2017, puede instalar y administrar paquetes de R mediante T-SQL. Para obtener más información, consulte [instalar y administrar paquetes de R](../r/install-additional-r-packages-on-sql-server.md).

Para Python y en SQL Server 2016, un administrador debe instalar las bibliotecas adicionales que podrían ser necesarias.

> [!IMPORTANT]
> Si va a ejecutar el código de R en SQL Server, asegúrese de que instale los mismos paquetes en el equipo que desee utilizar para desarrollar la solución y la instancia de SQL Server en la que ejecutar o implementar la solución.

### <a name="upgrading-r-server-or-sql-server-machine-learning"></a>Actualizar el aprendizaje automático de R Server o SQL Server

Si no piensa usar SQL Server, puede instalar Microsoft R Server o servidor de aprendizaje de máquina mediante un instalador independiente de Windows. Para ubicaciones de descarga e instrucciones, vea los siguientes vínculos:

+ [Instalar para Windows Server de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar a R Server 9.0.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) 

También se puede usar el instalador independiente de windows para el servidor de aprendizaje de máquina para actualizar los componentes asociados con la instancia de aprendizaje automático.  Para obtener más información, vea estos vínculos:

+ [Utilice SqlBindR para actualizar R](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
