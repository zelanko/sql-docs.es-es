---
title: "Administración de paquetes de R para SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 10/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2b421ea34185f483bac0b9f3bd2527d68428bf50
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="r-package-management-for-sql-server"></a>Administración de paquetes de R para SQL Server

Este artículo describen características para la administración de paquetes de R en SQL Server 2017 y SQL Server 2016.

+ Cambios en los métodos de instalación de paquete de R entre 2016 y de 2017
+ Métodos recomendados para administrar paquetes de R
+ Nuevos roles de base de datos de administración de paquetes en SQL Server 2017
+ Nueva instrucción de T-SQL para administración de paquetes en SQL Server 2017

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="differences-in-package-management-between-sql-server-2016-and-sql-server-2017"></a>Diferencias en la administración de paquetes entre SQL Server 2016 y SQL Server 2017

En **SQL Server 2017**, puede habilitar la administración de paquetes en el nivel de instancia y administrar permisos de usuario para agregar o usar paquetes en el nivel de base de datos.

Esto requiere que el Administrador de base de datos habilite la característica de administración de paquetes mediante la ejecución de un script que crea los objetos de base de datos necesarios. Para obtener más información, consulte [cómo habilitar la administración de paquetes de R](r-package-how-to-enable-or-disable.md).

En **SQL Server 2016**, un administrador debe instalar paquetes de R en la biblioteca de R asociada a la instancia. Todos los usuarios ejecutar código R en la instancia Utilice estos paquetes. Código de R que se ejecuta en SQL server no puede utilizar paquetes instalados en bibliotecas de usuario. Sin embargo, el administrador puede conceder individuales a los usuarios la capacidad para ejecutar scripts de R en una base de datos.

**Resumen de las diferencias y ventajas**

+ Si está utilizando servicios de aprendizaje de máquina en SQL Server 2017, puede administrar e instalar paquetes de R mediante el método tradicional, basándose en las herramientas de R, o mediante el uso de las instrucciones de T-SQL y nuevos roles de base de datos.

+ Se recomienda que el último método, porque proporciona un control más minucioso de los administradores, junto con más libertad para los usuarios. Por ejemplo, los usuarios pueden instalar sus propios paquetes, ya sea mediante un procedimiento almacenado o a través de código de R y los paquetes de recurso compartido con otras personas. 

    Dado que los paquetes se pueden alcanzar a una base de datos y cada usuario obtenga un espacio aislado de paquete aislado, es más fácil instalar diferentes versiones del mismo paquete de R. También es posible puede copiar o mover los usuarios y sus paquetes entre las bases de datos. 

+ Uso de la característica de administración de paquetes en SQL Server hace que las operaciones de copia de seguridad y restauración mucho más fácil. Cuando se migra la base de datos de trabajo a un nuevo servidor, puede usar la función de sincronización de paquete para leer una lista de todos los paquetes e instalarlos en una base de datos en el nuevo servidor.

+ Le resultará más cómodo instalar paquetes de R como administrador en el equipo, mediante las herramientas tradicionales de R, si es la única persona que utiliza el servidor para trabajos de aprendizaje de máquina.

+ Si usas SQL Server 2016 R Services, debe seguir instalar paquetes de R usados por la instancia con herramientas de R > Asegúrese de usar la biblioteca de R asociada a la instancia.

En las secciones siguientes proporcionan más detalles sobre cómo la administración de paquetes realiza utilizando estas dos opciones.

## <a name="r-package-management-using-t-sql"></a>Administración de paquetes de R mediante T-SQL

SQL Server 2017 incluye nuevas instrucciones de T-SQL que ofrecen lo DBA más control sobre los paquetes de R en el nivel de base de datos. Al mismo tiempo, el DBA puede permitir que los usuarios la capacidad para instalar los paquetes que necesitan y compartan con otras personas.

Si necesita compartir paquetes con otros usuarios, o si necesitan varias personas ejecutar trabajos de aprendizaje de máquina en el servidor, se recomienda habilitar la administración de paquetes, asignar a usuarios a roles de base de datos y cargar los paquetes para que los usuarios puedan compartirlos.

Administración de paquetes en SQL Server 2017 se basa en estos nuevos objetos de base de datos y características:

+ Nuevos roles de base de datos, para la administración de uso y acceso al paquete
+ Ámbito de paquete para paquetes privados e independientes compartido
+ Declaración de crear una biblioteca externa, de carga nuevas bibliotecas de código en el servidor
+ Contexto de proceso de nuevas funciones de RevoScaleR para admitir la instalación de paquetes en un servidor SQL Server R
+ Sincronización de paquetes, para garantizar una copia de seguridad y restauración de paquetes

### <a name="database-roles-for-package-management"></a>Roles de base de datos para la administración de paquetes

El Administrador de base de datos debe crear los roles utilizados para la administración de paquetes mediante la ejecución de una secuencia de comandos como se describe aquí: [habilitar o deshabilitar la administración de paquetes](r-package-how-to-enable-or-disable.md).

Después de ejecutar este script, debería ver los nuevos roles de base de datos siguientes:

+ `rpkgs-users`: Los miembros de este rol pueden utilizar cualquier paquete compartido que fue instalado por otro `rpkgs-shared` miembro del rol.

+ `rpkgs-private`: Los miembros de este rol tienen acceso a los paquetes compartidos, con los mismos permisos que los miembros de los `rpkgs-users` rol. Miembros de este rol también pueden instalar, quitar y usar paquetes de forma privada con ámbito.

+ `rpkgs-shared`: Los miembros de este rol tienen los mismos permisos que los miembros de los `rpkgs-private` rol. Además, los miembros de este rol pueden instalar o quitar paquetes compartidos.

+ `db_owner`: Los miembros de este rol tienen los mismos permisos que los miembros de los `rpkgs-shared` rol. Además, los miembros de este rol pueden **conceder** otros usuarios la posibilidad de instalar o quitar ambos compartida y paquetes privados.

El DBA agrega los usuarios a los roles en una base de cada base de datos, para controlar la capacidad del usuario para instalar paquetes.

### <a name="package-scope"></a>Ámbito del paquete

Las nuevas características de administración del paquete distinguen paquetes según si son privados, o puede ser compartidos por varios usuarios.

+ **Ámbito compartido**

    *Ámbito compartido* significa que los usuarios que le ha concedido permiso a la función de ámbito compartido (`rpkgs-shared`) pueden instalar y desinstalar paquetes a una base de datos especificada. Un paquete que se instala en una biblioteca de ámbito compartido lo pueden usar otros usuarios de la base de datos en SQL Server, siempre y cuando estos usuarios tengan permiso para usar paquetes de R instalados.

+ **Ámbito privado**

    *Ámbito privado* significa que los usuarios que se han proporcionado con pertenencia en el rol de ámbito privado (`rpkgs-private`) puede instalar o desinstalar paquetes en una ubicación de biblioteca privada definida por el usuario. Por lo tanto, los paquetes instalados en el ámbito privado solo los puede usar el usuario que los instaló. Dicho de otra manera, un usuario de SQL Server no puede usar los paquetes privados que instaló otro usuario.

Estos modelos de ámbito *compartido* y *privado* se pueden combinar para desarrollar sistemas seguros personalizados para implementar y administrar paquetes en SQL Server.

Por ejemplo, con el ámbito compartido, el jefe o el administrador de un grupo de científicos de datos podría recibir permiso para instalar paquetes, que luego podrían usar el resto de los usuarios o de los científicos de datos en la misma instancia de SQL Server.

En otro escenario se podría necesitar más aislamiento entre los usuarios o se tendrían que usar diferentes versiones de paquetes. En ese caso, el ámbito privado se puede usar para asignar permisos a los científicos de datos, que se encargarían de instalar y usar únicamente los paquetes que necesitan. Dado que los paquetes se instalan para cada usuario, los paquetes que instale un usuario no afectarán al trabajo del resto de los usuarios que usan la misma base de datos de SQL Server.

### <a name="create-external-library"></a>CREAR BIBLIOTECA EXTERNA

El [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) es una nueva instrucción de T-SQL introducida en SQL Server 2017 para ayudar al administrador de base de datos trabajar con paquetes sin necesidad de herramientas de usuario R. 

Usa el **crear biblioteca externa** instrucción para cargar bibliotecas externas a una instancia en el formato de archivo comprimido. Los usuarios autorizados, a continuación, pueden tener acceso a las bibliotecas e instalarlas para su propio uso.

Por ejemplo, podría crear varias copias del proyecto R, cada uno con una versión diferente. Cargarlos como bibliotecas independientes le permite mantener la privacidad de algunas versiones y compartir algunas versiones con otros usuarios.

Un "library" básicamente es una colección de paquetes externos que desea poner a disposición de los usuarios con un nombre único. Por ejemplo, podría publicar cualquiera de las siguientes acciones a SQL Server como una biblioteca externa:

+ Un único paquete de R que se haya escrito, no tiene dependencias
+ Un paquete que desea instalar y las dependencias necesarias para la instalación
+ Una colección de paquetes de R relacionados con una tarea específica o un proyecto, con sus dependencias

El nombre de la biblioteca es para administrar el paquete o una colección de paquetes en SQL Server y puede ser independiente de los paquetes que están instalados. Sin embargo, los nombres de biblioteca deben ser únicos en una instancia.

Para utilizar esta instrucción, la característica de administración de paquetes debe haber habilitado en la instancia. Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

> [!NOTE]
> Actualmente se puede utilizar esta instrucción para crear bibliotecas sólo basadas en Windows para compatibilidad con R. se ha planeado en el futuro para los paquetes de Python y para los paquetes que se ejecutan en otras plataformas, como Linux.

Después de que se ha cargado la biblioteca externa en el servidor, debe instalarlo en la biblioteca de paquetes de R asociada a la instancia. Hay varias maneras de hacerlo:

+ Ejecute el comando estándar de R `install.packages` en sp_execute_external_script. Asegúrese de conectar con una cuenta que tenga permisos para instalar paquetes.

+ Conectarse a SQL Server desde un cliente remoto de R y ejecute [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) en el contexto de proceso de SQL Server. De nuevo, debe tener permisos para instalar paquetes en ámbito privado o compartido para hacerlo.

Para ver ejemplos de instalación mediante R y T-SQL, consulte [instalar paquetes adicionales en SQL Server](install-additional-r-packages-on-sql-server.md).

### <a name="new-r-functions-for-package-installation"></a>Nuevas funciones de R para la instalación del paquete

Después de que se han habilitado los roles de base de datos de administración de paquetes, los usuarios también pueden usar nuevas funciones en [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) para instalar paquetes en la instancia especificada como el contexto de proceso de SQL Server.

+ Los científicos de datos pueden instalar paquetes de R necesarios en SQL Server sin necesidad de acceso directo en el equipo de SQL Server.

+ Un usuario puede instalar un paquete y compartir con otros usuarios, al instalar el paquete con ámbito compartido. A continuación, otros usuarios autorizados de la misma base de datos de SQL Server pueden tener acceso al paquete.

+ Los usuarios pueden instalar paquetes privados que no son visibles para otros usuarios, crear un espacio aislado privado paquetes de R.

Se proporcionan las siguientes funciones de administración de paquetes en RevoScaleR, para la instalación y eliminación de paquetes en un contexto de proceso especificado:

-   [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): buscar información acerca de los paquetes instalados en el contexto de proceso especificado.

-   [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): instalar paquetes en un contexto de proceso, ya sea desde un repositorio especificado o leyendo guardados localmente zip paquetes.

-   [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): quitar los paquetes instalados en un contexto de proceso.

-   [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): obtener la ruta de acceso para uno o varios paquetes en el contexto de proceso especificado.

-   [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): copia de una biblioteca de paquetes entre el sistema de archivos y bases de datos en los contextos de proceso especificado.

-   [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): obtener la ruta de acceso de búsqueda para los árboles de biblioteca para los paquetes mientras se ejecuta dentro de SQL Server.

Para usar estas funciones, conéctese a una instancia de SQL Server que tiene los permisos necesarios, con un contexto de proceso de SQL Server. Cuando se conecta, las credenciales de determinan si se puede completar la operación en el servidor.

Las funciones de instalación de paquetes comprueban si hay dependencias y se aseguran de que se puedan instalar todos los paquetes relacionados en SQL Server, como la instalación de paquetes de R en el contexto de proceso local. La función que desinstala los paquetes también calcula las dependencias y se asegura de que se quiten los paquetes que otros paquetes de SQL Server ya no usan, con el objetivo de liberar recursos.

> [!NOTE]
> 
> Estas nuevas funciones se incluyen de forma predeterminada en SQL Server 2017. Puede actualizar su versión de RevoScaleR para obtener estas funciones mediante la actualización de la instancia para que utilice una versión posterior de Microsoft R Server, como Microsoft R Server 9.0.1.
> 
> Para obtener más información, consulte [utilizando SqlBindR.exe al actualizador de](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="synchronization-of-r-package-libraries"></a>Sincronización de las bibliotecas de paquete de R

La versión 2.0 de CTP de SQL Server 2017 (y la versión de abril de 2017 de Microsoft R Server) incluye nuevas funciones de R para *sincronizar paquetes*.

Sincronización de paquete significa que el motor de base de datos realiza un seguimiento de los paquetes que usan un propietario específico y un grupo y pueden escribir estos paquetes en el sistema de archivos si es necesario. Puede utilizar la sincronización de paquete en estos escenarios:

+ Desea mover los paquetes de R entre instancias de SQL Server.
+ Debe volver a instalar los paquetes para un usuario específico o grupo después de restaura una base de datos.

Para obtener más información acerca de cómo habilitar y usar esta característica, consulte [sincronización de paquetes de R para SQL Server](package-install-uninstall-and-sync.md).

## <a name="r-package-management-using-traditional-r-tools"></a>Administración de paquetes de R mediante herramientas tradicionales de R

El método tradicional de la administración de paquetes de R en una instancia es instalar y enumerar paquetes mediante comandos y herramientas de R. 

+ Esta opción puede ser la única opción si está utilizando una versión preliminar de SQL Server 2016.  
+ Esta opción también puede ser conveniente si es el único usuario de paquetes de R y tiene acceso administrativo al servidor.
+ Para facilitar la administración de las versiones de paquetes de R, puede usar [miniCRAN](create-a-local-package-repository-using-minicran.md) para crear un repositorio local y compartirlo entre las instancias.

Para obtener más información, vea estos artículos:

+ [Instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md)
+ [Determinación de los paquetes instalados en SQL Server](determine-which-packages-are-installed-on-sql-server.md)

Para SQL Server 2017, recomendamos que utilice crear biblioteca externa y los roles de base de datos proporciona para administrar usuarios y sus paquetes de R.

## <a name="next-steps"></a>Pasos siguientes

[Cómo habilitar o deshabilitar la administración de paquetes de R](../r/r-package-how-to-enable-or-disable.md)
