---
title: Paquetes de R instalados con SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0e96334850554ab642e3372c3631f3ab672109d6
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="r-packages-installed-with-sql-server"></a>Paquetes de R instalados con SQL Server

Este artículo describe los paquetes de R que se instalan con SQL Server y proporciona información sobre cómo administrar y ver los paquetes existentes.

En este artículo también proporciona vínculos a información sobre cómo agregar nuevos paquetes para su uso con SQL Server.

**Se aplica a:** servicios de aprendizaje de máquina SQL Server de 2017 (en bases de datos), SQL Server 2016 R Services (In-Database)

## <a name="what-is-the-instance-library-and-where-is-it"></a>¿Qué es la biblioteca de la instancia y donde se?

Cualquier solución de R que se ejecuta en SQL Server puede usar solo los paquetes que están instalados en la biblioteca de R predeterminado asociada a la instancia.

Cuando se instalación características de R en SQL Server, la biblioteca de paquetes de R se encuentra en la carpeta de la instancia.

+ Instancia predeterminada *MSSQLSERVER* 

    2017 de SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ Instancia con nombre *MyNamedInstance* 

    2017 de SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

Puede ejecutar la siguiente instrucción para comprobar la biblioteca predeterminada de la instancia actual de R.

```SQL
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```
## <a name="r-packages-installed-with-sql-server"></a>Paquetes de R instalados con SQL Server

Cuando instala el lenguaje R en SQL Server, de forma predeterminada la R **base** paquetes instalados. Paquetes base incluyen funcionalidad básica proporcionada por paquetes como `stats` y `utils`.

Instalación de R en SQL Server 2016 y SQL Server 2017 también incluye el **RevoScaleR** paquete y paquetes mejorados relacionados y los proveedores, que es compatible con contextos de proceso remoto, transmisión por secuencias, ejecución de la función rx, en paralelo y muchas otras características.

+ Para obtener información general de las características mejoradas de R, consulte [sobre el servidor de aprendizaje de máquina](https://docs.microsoft.com/r-server/what-is-microsoft-r-server)

+ Para descargar las bibliotecas de RevoScaleR en un equipo cliente, instale [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>Permisos necesarios para instalar paquetes de R

En SQL Server 2016, un administrador tenía que instalar nuevos paquetes de R según una sola instancia. En SQL Server 2017, se agregaron nuevas características de base de datos que permiten al administrador de base de datos de la capacidad para delegar la administración de paquetes a los usuarios seleccionados.

En esta sección se describe los permisos necesarios para instalar y administrar paquetes por versión.

+ SQL Server 2016 R Services (In-Database)

    Para instalar un nuevo paquete de R en un equipo que ejecuta [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], debe tener derechos administrativos en el equipo. Es la tarea del Administrador de base de datos o de otro administrador en el servidor para asegurarse de que todos los paquetes necesarios están instalados en el [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instancia.

    Si no tiene privilegios administrativos en el equipo que hospeda el [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instancia, puede proporcionar a la información del administrador acerca de cómo instalar paquetes de R y proporcionar acceso a un repositorio de paquetes seguro donde los paquetes solicitado por los usuarios se pueden obtener.

+ SQL Server 2017 Machine Learning Services

    Esta versión incluye las funciones de administración del paquete que permiten que el Administrador de base de datos delegar derechos de instalación de paquete a los usuarios seleccionados. Si se ha habilitado esta característica, solicite que el Administrador de base de datos agregue a uno de los nuevos roles de paquete. Para obtener más información, consulte [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md).

    Si es administrador en la instancia de SQL Server, puede instalar nuevos paquetes como desee. Asegúrese de usar la biblioteca predeterminada que está asociada a la instancia. Cuando se llama desde un procedimiento almacenado, no se pueden ejecutar paquetes instalados en otras ubicaciones. Cualquier código de R que se ejecuta con el servidor SQL Server como un contexto de proceso también requiere que los paquetes estén disponibles en la biblioteca de la instancia.

+ R Server (Standalone)

    Necesitará derechos administrativos en el equipo para instalar nuevos paquetes de R.

+ Otros entornos de cliente

    Si va a instalar un nuevo paquete de R en un equipo que está en uso como una estación de trabajo de R y el equipo no **no** tiene una instancia de [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] , también necesitará derechos administrativos en el equipo Instale el paquete. Después de instalar el paquete, puede ejecutarlo en el entorno local.

## <a name="managing-or-viewing-installed-packages"></a>Administrar o ver los paquetes instalados

Hay varias maneras en que puede obtener una lista completa de los paquetes instalados actualmente. Para obtener más información, consulte [determinar qué paquetes están instalados en SQL Server](determine-which-packages-are-installed-on-sql-server.md).

