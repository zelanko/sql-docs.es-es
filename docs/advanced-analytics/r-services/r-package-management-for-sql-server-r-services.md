---
title: "R Package Management for SQL Server R Services (Administraci&#243;n de paquetes de R para SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# R Package Management for SQL Server R Services (Administraci&#243;n de paquetes de R para SQL Server R Services)
Para facilitar la administración de paquetes de R que se ejecutan en una instancia de SQL Server, el paquete **RevoScaleR** ahora incluye funciones para admitir la instalación y la administración de paquetes de R. 

Esta nueva funcionalidad admite varios escenarios:

- El científico de datos puede instalar un paquete de R necesario en SQL Server sin tener acceso administrativo al equipo de SQL Server. Los paquetes se instalan según las bases de datos respectivas.
- Compartir paquetes con otros usuarios es fácil. Solo tiene que establecer un repositorio de paquetes local y hacer que cada científico de datos instale los paquetes en cada base de datos.
- El administrador de la base de datos no tiene que aprender a ejecutar comandos de R ni comprender las dependencias de las paquetes. El administrador de la base de datos usa los roles de base de datos para controlar los usuarios de SQL Server que pueden instalar, desinstalar o usar los paquetes.
 
**Funcionamiento**

* El administrador de la base de datos se encarga de configurar los roles y de agregar usuarios a los roles para controlar quién tiene permiso para agregar o quitar paquetes de R en el entorno de SQL Server.
* Si tiene permiso para instalar paquetes, ejecute una de las funciones de administración de paquetes desde el código de R y especifique el contexto de proceso en el que se deben agregar o quitar los paquetes. El contexto de proceso puede ser el equipo local o una base de datos de la instancia de SQL Server. 
* Si la llamada a la instalación de paquetes se ejecuta en SQL Server, las credenciales determinan si se puede llevar a cabo la operación en el servidor. 
- Las funciones de instalación de paquetes comprueban si hay dependencias y se aseguran de que se puedan instalar todos los paquetes relacionados en SQL Server, como la instalación de paquetes de R en el contexto de proceso local.
- La función que desinstala los paquetes también calcula las dependencias y se asegura de que se quiten los paquetes que otros paquetes de SQL Server ya no usan, con el objetivo de liberar recursos.
- Cada científico de datos puede instalar paquetes privados que no sean visibles para el resto de los usuarios, lo que les proporciona un espacio aislado para trabajar con sus propios paquetes de R.
-  Dado que los paquetes pueden tener como ámbito una base de datos y cada usuario obtiene un espacio aislado de paquetes en cada base de datos, resulta más fácil instalar versiones diferentes del mismo paquete de R. 

> [!NOTE]
> Actualmente, esta característica solo se ha publicado para su uso con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. 

## <a name="database-roles-and-database-scoping"></a>Roles y ámbitos de la base de datos

Las nuevas funciones de administración de paquetes proporcionan dos ámbitos para instalar y usar paquetes en SQL Server en una base de datos determinada:

- **Ámbito compartido**

  *Ámbito compartido* significa que los usuarios a los que se ha concedido permiso en el rol de ámbito compartido (**rpkgs-shared**) pueden instalar y desinstalar paquetes en una base de datos especificada. Un paquete que se instala en una biblioteca de ámbito compartido lo pueden usar otros usuarios de la base de datos en SQL Server, siempre y cuando estos usuarios tengan permiso para usar paquetes de R instalados. 

- **Ámbito privado** 

  *Ámbito privado* significa que los usuarios que disponen de pertenencia en el rol de ámbito privado (**rpkgs-private**) pueden instalar o desinstalar paquetes en una ubicación de biblioteca privada definida por cada usuario. Por lo tanto, los paquetes instalados en el ámbito privado solo los puede usar el usuario que los instaló. Dicho de otra manera, un usuario de SQL Server no puede usar los paquetes privados que instaló otro usuario. 

Estos modelos de ámbito *compartido* y *privado* se pueden combinar para desarrollar sistemas seguros personalizados para implementar y administrar paquetes en SQL Server. 

Por ejemplo, con el ámbito compartido, el jefe o el administrador de un grupo de científicos de datos podría recibir permiso para instalar paquetes, que luego podrían usar el resto de los usuarios o de los científicos de datos en la misma instancia de SQL Server. 

En otro escenario se podría necesitar más aislamiento entre los usuarios o se tendrían que usar diferentes versiones de paquetes. En ese caso, el ámbito privado se puede usar para asignar permisos a los científicos de datos, que se encargarían de instalar y usar únicamente los paquetes que necesitan. Dado que los paquetes se instalan para cada usuario, los paquetes que instale un usuario no afectarán al trabajo del resto de los usuarios que usan la misma base de datos de SQL Server. 

### <a name="database-roles-for-package-management"></a>Roles de base de datos para la administración de paquetes

Los siguientes roles de base de datos nuevos admiten una instalación segura y la administración de paquetes para SQL R Services: 

- **rpkgs-users**: permite a los usuarios usar cualquier paquete compartido que los miembros del rol **rpkgs-shared** hayan instalado.

- **rpkgs-private**: proporciona acceso a los paquetes compartidos con los mismos permisos que el rol **rpkgs-users**. Los miembros de este rol también pueden instalar, quitar y usar paquetes de ámbito privado.

-  **rpkgs-shared**: proporciona los mismos permisos que el rol **rpkgs-private**. Los usuarios que son miembros de este rol también pueden instalar o quitar paquetes compartidos. 
 
- **db_owner**: tiene los mismos permisos que el rol **rpkgs-shared**. También puede conceder a los usuarios el derecho de instalar o quitar paquetes compartidos y privados.



## <a name="new-package-management-functions"></a>Nuevas funciones de administración de paquetes


+ `rxInstalledPackages`: obtenga información sobre los paquetes instalados en el contexto de proceso especificado.

+ `rxInstallPackages`: instale los paquetes en un contexto de proceso, ya sea desde un repositorio especificado o leyendo paquetes comprimidos guardados de forma local.

+ `rxRemovePackages`: elimine los paquetes instalados desde un contexto de proceso.

+ `rxFindPackage`: obtenga la ruta de acceso de uno o varios paquetes en el contexto de proceso especificado.

+ `rxSqlLibPaths`: obtenga la ruta de búsqueda de los árboles de biblioteca de los paquetes mientras se ejecutan en SQL Server.

## <a name="examples"></a>Ejemplos

### <a name="get-package-location-on-sql-server-compute-context"></a>Obtener la ubicación de los paquetes en el contexto de proceso de SQL Server

En este ejemplo se obtiene la ruta de acceso del paquete **RevoScaleR** en el contexto del proceso, *sqlServer*.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```
  
  ### <a name="get-locations-for-multiple-packages"></a>Obtener la ubicación de varios paquetes

En el ejemplo siguiente se obtienen las rutas de acceso de los paquetes **RevoScaleR** y **lattice** en el contexto de proceso, *sqlServer*. Al buscar información sobre varios paquetes, pase un vector de cadena que contenga el nombre de los paquetes.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```



### <a name="list-packages-in-specified-compute-context"></a>Enumerar los paquetes en el contexto de proceso especificado

En este ejemplo se enumeran y se muestran en la consola todos los paquetes instalados en el contexto de proceso, *sqlServer*.

  ```R
  myPackages <- rxInstalledPackages(computeContext = sqlServer) 
  myPackages
  ```

### <a name="get-package-versions"></a>Obtener la versión de los paquetes

En este ejemplo se obtiene el número de compilación y los números de versión de un paquete instalado en el contexto de proceso, *sqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer) 
```

### <a name="install-a-package-on-sql-server"></a>Instalar un paquete en SQL Server

En este ejemplo se instala el paquete **ggplot2** y sus dependencias en el contexto de proceso, *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>Quitar un paquete de SQL Server

En este ejemplo se quita el paquete **ggplot2** y sus dependencias del contexto de proceso, *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

## <a name="see-also"></a>Vea también

[Cómo habilitar o deshabilitar la administración de paquetes de R](../../advanced-analytics/r-services/how-to-enable-or-disable-r-package-management.md)