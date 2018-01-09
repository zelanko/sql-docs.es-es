---
title: "Administración de paquetes de R para SQL Server | Documentos de Microsoft"
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
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 576178e53a28f877ac91d99f14ce9ba6a44e506d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="r-package-management-for-sql-server"></a>Administración de paquetes de R para SQL Server

Este artículo describen características para la administración de paquetes de R en SQL Server 2017 y en SQL Server 2016.

+ Métodos recomendados para administrar paquetes de R (y paquetes Python)
+ Cambios en la administración de paquetes entre SQL Server 2016 y de 2017

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="recommended-methods-for-package-management"></a>Métodos recomendados para la administración de paquetes

En SQL Server 2016 y 2017 de SQL Server, un administrador del equipo puede instalar paquetes para cada instancia donde se ha habilitado el aprendizaje automático. 

Los paquetes se instalan en el sistema de archivos mediante las bibliotecas de instancia y no puede compartirse en todas las instancias. Actualmente, esta es el método recomendado para SQL Server 2016 y 2017 de SQL Server.

+ [Instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md)
+ [Determinación de los paquetes instalados en SQL Server](determine-which-packages-are-installed-on-sql-server.md)

Además, si tiene **dbo** pertenencia a una función en una instancia de SQL Server donde se ha habilitado el aprendizaje automático, puede instalar paquetes de R desde un cliente remoto, mediante el uso de nuevas funciones de RevoScaleR.

+ [Nuevas funciones de R para la instalación del paquete](#bkmk_remoteInstall)

### <a name="installation-on-servers-with-no-internet-access"></a>Instalación en servidores sin acceso a Internet

Para que sea más fácil de determinar las versiones necesarias de paquete de R y proporcionar todas las dependencias del paquete, puede usar [miniCRAN](https://mran.microsoft.com/package/miniCRAN). Este paquete de R toma una lista de los paquetes de destino y crea un repositorio local que contiene los paquetes de destino junto con todas sus dependencias, en formato comprimido. A continuación, puede copie en el servidor sin conexión, o compartir el repositorio entre varias instancias.

Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="python-packages"></a>Paquetes de Python

Instalación de nuevos paquetes de Python sigue las mismas directrices: 

+ Revisar los paquetes de Python de antemano para determinar la compatibilidad con la versión actual de Python
+ Evaluar la adecuación de paquete de Python para un entorno de SQL Server protegido
+ Utilice las herramientas Python para instalar paquetes como un administrador
+ Instalar los paquetes que se deben ejecutar en el contexto de SQL Server sólo en la biblioteca de la instancia. 
+ Si utiliza varios entornos para pruebas, producción, etc., asegúrese de que está instalada la misma versión del paquete de Python en la biblioteca de la instancia.

Para obtener pasos de instalación, consulte [instalar nuevos paquetes de Python en SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="features-for-package-management-in-sql-server-2016-and-sql-server-2017"></a>Características de administración de paquetes en SQL Server 2016 y SQL Server 2017

SQL Server 2017 agrega algunas características nuevas para admitir la administración sea más fácil de paquetes de R (y Python) por los administradores de base de datos. Estas características nuevas incluyen:

+ La capacidad para instalar o administrar las bibliotecas de paquete mediante T-SQL
+ Administración de permisos de usuario en el nivel de base de datos a través de roles de base de datos. 

En versiones futuras, estas características se espera que proporcione el método principal para la administración de paquetes por los administradores de base de datos y facilitar a los científicos de datos instalar las bibliotecas que necesitan.

En aproximadamente al mismo tiempo, Microsoft R Server y servidor de aprendizaje de máquina agregan nuevas funciones de R para que resulten más fáciles de instalar y compartir los paquetes en un contexto de proceso de SQL Server. Estas funciones funcionan independientemente de las características de SQL Server en función de T-SQL y están diseñadas para ejecutarse desde un cliente remoto de R.

Esta sección proporciona información general de estas características.

### <a name="bkmk_remoteInstall"></a>Nuevas funciones de RevoScaleR para la instalación del paquete 

Los usuarios con una versión reciente de R Server o servidor de aprendizaje de máquina también pueden usar nuevas funciones en [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) para instalar paquetes en una instancia especificada como el contexto de proceso de SQL Server.

+ Los científicos de datos pueden instalar paquetes de R necesarios en SQL Server sin necesidad de acceso directo en el equipo de SQL Server. Sin embargo, el usuario debe ser miembro del propietario de base de datos (**dbo**) rol.

+ El usuario puede compartir paquetes con otros usuarios, mediante la instalación de paquetes con ámbito compartido. Otros usuarios autorizados de la misma base de datos de SQL Server pueden tener acceso al paquete.

+ Los usuarios pueden instalar paquetes privados que no son visibles para otros usuarios, crear un espacio aislado privado paquetes de R.

+ Sincronización de paquetes permite fácilmente copias de seguridad y restauración de paquetes

#### <a name="package-installation-functions"></a>Funciones de instalación de paquete

Se proporcionan las siguientes funciones de administración de paquetes en RevoScaleR, para la instalación y eliminación de paquetes en un contexto de proceso especificado:

-   [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages): buscar información acerca de los paquetes instalados en el contexto de proceso especificado.

-   [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages): instalar paquetes en un contexto de proceso, ya sea desde un repositorio especificado o leyendo guardados localmente zip paquetes.

-   [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages): quitar los paquetes instalados en un contexto de proceso.

-   [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage): obtener la ruta de acceso para uno o varios paquetes en el contexto de proceso especificado.

-   [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages): copia de una biblioteca de paquetes entre el sistema de archivos y bases de datos en los contextos de proceso especificado.

-   [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): obtener la ruta de acceso de búsqueda para los árboles de biblioteca para los paquetes mientras se ejecuta dentro de SQL Server.

Para usar estas funciones, conéctese a una instancia de SQL Server que tiene los permisos necesarios, con un contexto de proceso de SQL Server. 

> [!IMPORTANT]
> Las credenciales que use en la conexión de determinan si se puede completar la operación en el servidor.

Estas funciones de instalación de paquete comprobación las dependencias y asegúrese de que se pueden instalar todos los paquetes relacionados con SQL Server, igual que la instalación del paquete de R en el contexto de proceso local. La función que desinstala los paquetes también calcula las dependencias y se asegura de que se quiten los paquetes que otros paquetes de SQL Server ya no usan, con el objetivo de liberar recursos.

Estas nuevas funciones se incluyen en la versión de RevoScaleR que se instala en SQL Server 2017. También puede obtener estas funciones [actualizar la instancia de SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) para utilizar una versión reciente de [Microsoft R Server o servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server). Requiere la versión 9.0.1 o una versión posterior.

#### <a name="package-synchronization-functions"></a>Funciones de sincronización de paquete

Sincronización de paquetes es una característica nueva para los paquetes de R solo. El motor de base de datos realiza un seguimiento de los paquetes que usan un propietario específico y un grupo y pueden escribir estos paquetes en el sistema de archivos si es necesario. Normalmente se usaría sincronización de paquetes en estos escenarios:

+ Desea mover los paquetes de R entre instancias de SQL Server.
+ Debe volver a instalar los paquetes para un usuario específico o grupo después de restaura una base de datos.

Para obtener más información acerca de cómo habilitar y usar esta característica, consulte [sincronización de paquetes de R para SQL Server](package-install-uninstall-and-sync.md).

### <a name="package-management-using-t-sql"></a>Administración de paquetes mediante T-SQL

SQL Server 2017 agrega las nuevas instrucciones T-SQL para proporcionar a lo DBA más control sobre los paquetes de R en el nivel de base de datos. El DBA no debería tener que aprender a usar R o herramientas de Python, pero en su lugar, debe ser capaz de ofrecer a los usuarios de R o Python la capacidad para instalar los paquetes que necesitan y compartan con otras personas.

Esta característica está diseñada para facilitar la colaboración y la versión de la administración en entornos multiusuario: por ejemplo:

+ Desea compartir los paquetes que han desarrollado con otras personas de su equipo.
+ Los analistas varios están trabajando en la misma base de datos y necesitan usar diferentes versiones del mismo paquete.
+ Desea mover los paquetes y sus permisos a la vez que se mueve una base de datos o al realizar la copia de seguridad y las operaciones de restauración.

Administración de paquetes en SQL Server 2017 se basa en estos nuevos objetos de base de datos y características:

+ [Nuevos roles de base de datos](#bkmk_roles), para la administración de acceso del paquete y usar
+ [CREAR una biblioteca externa](#bkmk_createExternalLibrary) instrucción para cargar bibliotecas de paquete en el servidor

El uso de estas características requiere cierta preparación adicional en el nivel de base de datos y la instancia: 

+  El Administrador de base de datos debe habilitar explícitamente la característica de administración de paquetes mediante la ejecución de un script que crea los objetos de base de datos necesarios. Para obtener más información, consulte [cómo habilitar la administración de paquetes de R](r-package-how-to-enable-or-disable.md).

+ Los usuarios deben asignarse a los roles, en un nivel de cada base de datos. Estas funciones dan a los usuarios la capacidad para instalar paquetes compartidos o privados.

+ Bibliotecas de paquete se pueden instalar con la nueva instrucción de T-SQL, crear una biblioteca externa. Sin embargo, todas las dependencias de paquete deben preparadas de antemano y se instala como parte de un solo archivo comprimido.

> [!NOTE]
> Aunque las características descritas aquí son totalmente funcionales en este momento, las versiones futuras contienen mejoras adicionales para que sea más fácil para preparar las bibliotecas de paquete y para administrar las dependencias. Si está familiarizado con la instalación del paquete de R, se recomienda que intenta utilizar las herramientas de R por ahora.

#### <a name="bkmk_createExternalLibrary"></a>CREAR BIBLIOTECA EXTERNA 

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

Para asegurarse de que se proporcionan todas las dependencias de paquete, se recomienda usar [miniCRAN](create-a-local-package-repository-using-minicran.md) para crear un repositorio local. A continuación, puede usar ese archivo comprimido para instalar el paquete de destino y sus dependencias.

#### <a name="bkmk_roles"></a>Roles de base de datos de administración de paquetes 

Los nuevos roles proporcionados en SQL Server para la administración de paquetes no se incluyen de forma predeterminada, incluso en casos donde se ha instalado y habilitado aprendizaje automático. Debe agregar los roles mediante la ejecución de una secuencia de comandos como se describe aquí: [habilitar o deshabilitar la administración de paquetes](r-package-how-to-enable-or-disable.md).

Después de ejecutar este script, debería ver los nuevos roles de base de datos siguientes:

+ `rpkgs-users`: Los miembros de este rol pueden utilizar cualquier paquete compartido que fue instalado por otro `rpkgs-shared` miembro del rol.

+ `rpkgs-private`: Los miembros de este rol tienen acceso a los paquetes compartidos, con los mismos permisos que los miembros de los `rpkgs-users` rol. Miembros de este rol también pueden instalar, quitar y usar paquetes de forma privada con ámbito.

+ `rpkgs-shared`: Los miembros de este rol tienen los mismos permisos que los miembros de los `rpkgs-private` rol. Además, los miembros de este rol pueden instalar o quitar paquetes compartidos.

+ `db_owner`: Los miembros de este rol tienen los mismos permisos que los miembros de los `rpkgs-shared` rol. Además, los miembros de este rol pueden **conceder** otros usuarios la posibilidad de instalar o quitar ambos compartida y paquetes privados.

El DBA puede agregar usuarios a funciones en una base de cada base de datos.



## <a name="next-steps"></a>Pasos siguientes

[Administración de paquetes para el aprendizaje automático de SQL Server](r-package-management-for-sql-server-r-services.md)