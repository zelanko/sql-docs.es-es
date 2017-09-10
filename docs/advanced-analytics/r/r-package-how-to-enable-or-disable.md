---
title: "Cómo habilitar o deshabilitar la administración de paquetes de R | Microsoft Docs"
ms.custom: 
ms.date: 12/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aac055d9a2337f1278d648fbcd17435afe1bd3b3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="r-package---how-to-enable-or-disable"></a>Paquete de R - Cómo habilitarlo y deshabilitarlo

De forma predeterminada, la administración de paquetes está deshabilitada en una instancia de SQL Server, aunque R Services esté instalado. La habilitación de esta característica es un proceso de dos pasos que debe realizar un administrador de base de datos: 

1. Habilitar la administración de paquetes en la instancia de SQL Server (una vez por instancia de SQL Server) 
2. Habilitar la administración de paquetes en la base de datos SQL (una vez por base de datos SQL Server) 


Al deshabilitar la característica de administración de paquetes, invierta el proceso de quitar los permisos y los paquetes de nivel de base de datos y, luego, quite los roles del servidor:
 
1. Deshabilitar la administración de paquetes en cada base de datos (una vez por base de datos) 
2. Deshabilitar la administración de paquetes en la instancia de SQL Server (una vez por instancia) 

> [!IMPORTANT]
> Esta característica está en desarrollo. Tenga en cuenta que la sintaxis o la funcionalidad pueden cambiar en versiones posteriores. 

### <a name="to-enable-package-management"></a>Para habilitar la administración de paquetes

La habilitación o deshabilitación de la administración de paquetes exige la utilidad de línea de comandos **RegisterRExt.exe**, incluida en el paquete **RevoScaleR** que se instala con SQL Server R Services. la ubicación predeterminada es:

`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` 
    
1. Abra un símbolo del sistema con privilegios elevados y use el siguiente comando:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando crea artefactos de nivel de instancia en el equipo de SQL Server que son necesarios para la administración de paquetes. 

2. Para agregar administración de paquetes en el nivel de base de datos, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados para cada base de datos en la que haya que instalar paquetes: 

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    Este comando crea algunos artefactos de base de datos, incluidos los siguientes roles de base de datos que son necesarios para controlar los permisos de usuario: **rpkgs-users**, **rpkgs-private**y **rpkgs-shared** 

### <a name="to-disable-package-management"></a>Para deshabilitar la administración de paquetes 

1. Desde un símbolo del sistema con privilegios elevados, ejecute el siguiente comando para deshabilitar la administración de paquetes en el nivel de base de datos:

   `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    Este comando quitará los artefactos de base de datos relacionados con la administración de paquetes de la base de datos especificada.  El comando también quitará todos los paquetes que se instalaron por base de datos desde la ubicación del sistema de archivos protegido en el equipo de SQL Server.
    
    El comando debe ejecutarse una vez por cada base de datos en la que se usara la administración de paquetes.
 
2. (Opcional) Para quitar completamente la característica de administración de paquetes de la instancia, después de quitar los paquetes de todas las bases de datos mediante el paso anterior, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita los artefactos de nivel de instancia usados por la administración de paquetes de la instancia de SQL Server. 


## <a name="see-also"></a>Vea también
[R Package Management for SQL Server R Services (Administración de paquetes de R para SQL Server R Services)](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)

