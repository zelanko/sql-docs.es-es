---
title: Paquetes de R instalados con SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 082aea3b1cde3c335dd7fa51b8ef219fc30f7efd
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="r-packages-installed-with-sql-server"></a>Paquetes de R instalados con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe los paquetes de R que se instalan con SQL Server si instala y habilita características de aprendizaje de la máquina. En este artículo también se describe cómo administrar y ver los paquetes existentes o agregar nuevos paquetes a una instancia de SQL Server.

**Se aplica a:** servicios de aprendizaje de máquina SQL Server de 2017 (en bases de datos), SQL Server 2016 R Services (In-Database)

## <a name="what-is-the-instance-library-and-where-is-it"></a>¿Qué es la biblioteca de la instancia y donde se?

Cualquier solución de R que se ejecuta en SQL Server puede usar solo los paquetes que están instalados en la biblioteca de R predeterminado asociada a la instancia. Cuando se instalación características de R en SQL Server, la biblioteca de paquetes de R se encuentra en la carpeta de la instancia.

+ Instancia predeterminada *MSSQLSERVER* 

    2017 de SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ Instancia con nombre *MyNamedInstance* 

    2017 de SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

Puede ejecutar la siguiente instrucción para comprobar la biblioteca predeterminada de la instancia actual de R.

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Alternatiely, puede usar la nueva [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) funcione, si la ejecución de sp\_ejecutar\_externo\_secuencia de comandos directamente en el equipo de destino. La función no puede devolver las rutas de acceso de biblioteca para las conexiones remotas.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
```

> [!NOTE]
> Si utiliza el enlace para actualizar los componentes de R en una instancia, puede cambiar la ruta de acceso a la biblioteca de la instancia. Asegúrese de comprobar la biblioteca en la que está usando SQL Server.

## <a name="r-packages-installed-with-sql-server"></a>Paquetes de R instalados con SQL Server

De forma predeterminada la R **base** paquetes instalados. Paquetes base incluyen funcionalidad básica proporcionada por paquetes como `stats` y `utils`.

Instalación de R en SQL Server 2016 o SQL Server 2017 siempre incluye la **RevoScaleR** paquete y paquetes mejorados relacionados y los proveedores, que es compatible con contextos de proceso remoto, transmisión por secuencias, ejecución de la función rx, en paralelo y muchas otras características. Para actualizar el paquete RevoScaleR, ya sea utilizar el enlace para actualizar solo los componentes, de aprendizaje de automático o revisiones o actualizar la instancia a una versión más reciente de SQL Server.

+ Para obtener información general de las características mejoradas de R, consulte [sobre el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ Para descargar las bibliotecas de RevoScaleR en un equipo cliente, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>Permisos necesarios para instalar paquetes de R

En SQL Server 2016, un administrador tenía que instalar nuevos paquetes de R según una sola instancia. 

SQL Server 2017 había presentado nuevas características para la instalación de paquete y administración:

+ Puede usar comandos de R desde un cliente remoto para instalar paquetes con ámbito privado o compartido. Esta característica necesita las palabras clave [Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install) o [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), así como de privilegios dbo en la instancia.
+ Se agregaron nuevas características de base de datos para admitir la administración del paquete por los administradores de base de datos sin usar T-SQL. En el futuro, estas características proporcionan los DBA con la capacidad para delegar la mayoría de las facetas de administración de paquetes a los usuarios con privilegios.

En esta sección se describe los permisos necesarios para instalar y administrar paquetes por versión.

+ SQL Server 2016 R Services (In-Database)

    Para instalar un nuevo paquete de R en un equipo que ejecuta [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], debe tener derechos administrativos en el equipo. Es la tarea del Administrador de base de datos o de otro administrador en el servidor para asegurarse de que todos los paquetes necesarios están instalados en el [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instancia.

    Si no tiene privilegios administrativos en el equipo que hospeda el [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instancia, puede proporcionar a la información del administrador acerca de cómo instalar paquetes de R y proporcionar acceso a un repositorio de paquetes seguro donde los paquetes solicitado por los usuarios se pueden obtener.

+ SQL Server 2017 Machine Learning Services

    Si es administrador en la instancia de SQL Server, puede instalar nuevos paquetes como desee. Asegúrese de usar la biblioteca predeterminada que está asociada a la instancia. Cuando se llama desde un procedimiento almacenado, no se pueden ejecutar paquetes instalados en otras ubicaciones. Cualquier código de R que se ejecuta con el servidor SQL Server como un contexto de proceso también requiere que los paquetes estén disponibles en la biblioteca de la instancia.

    Esta versión también incluye algunas características nuevas que se ha diseñado para admitir más fácil administración de paquetes mediante los DBA en una versión posterior. Por ahora, se recomienda que siga instalar paquetes de R en una base de toda la instancia.

+ R Server (Standalone)

    Necesitará derechos administrativos en el equipo para instalar nuevos paquetes de R.

+ Otros entornos de cliente

    Si va a instalar un nuevo paquete de R en un equipo que está en uso como una estación de trabajo de R y el equipo no **no** tiene una instancia de [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] , también necesitará derechos administrativos en el equipo Instale el paquete. Después de instalar el paquete, puede ejecutarlo en el entorno local.

## <a name="managing-or-viewing-installed-packages"></a>Administrar o ver los paquetes instalados

Hay varias maneras en que puede obtener una lista completa de los paquetes instalados actualmente. Para obtener más información, consulte [determinar qué paquetes están instalados en SQL Server](determine-which-packages-are-installed-on-sql-server.md).
