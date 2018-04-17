---
title: Bibliotecas de paquete para el aprendizaje automático en SQL Server predeterminadas | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 64b085c2314e4c97694e91924cb15d43315143e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="default-package-libraries-for-machine-learning-on-sql-server"></a>Bibliotecas de paquete para el aprendizaje automático en SQL Server predeterminadas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describen las bibliotecas predeterminadas para R y Python que se instala con SQL Server. Este artículo proporciona las ubicaciones predeterminadas de estas bibliotecas y explica cómo se pueden determinar qué paquetes y qué versión de R o Python se instala en cada biblioteca de instancia.

## <a name="using-the-default-instance-library"></a>Uso de la biblioteca de la instancia predeterminada

Cuando se instala el aprendizaje automático con SQL Server, se crea una biblioteca de paquete único en el nivel de instancia para cada idioma instalado. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas.

Si se conecta al servidor desde un cliente remoto, cualquier código de R o Python que desea ejecutar en el contexto de proceso de servidor puede usar solo los paquetes instalados en la biblioteca de la instancia.

Para proteger los activos del servidor, la biblioteca de la instancia predeterminada se instala en una carpeta protegida que se registra con SQL Server y se puede modificar únicamente por un administrador del equipo. Si no es el propietario del equipo, debe obtener el permiso de administrador para instalar paquetes a esta biblioteca. 

Incluso si usted es el propietario del equipo, debe considerar la utilidad de cualquier paquete de R o Python determinado en un entorno de servidor antes de agregar el paquete a la biblioteca de la instancia. Tenga en cuenta factores como el tamaño de los archivos de paquete y la necesidad de varias versiones, así como si requiere el paquete de red o internet access.

### <a name="sql-server"></a>SQL Server

|Versión | Nombre de instancia|Ruta de acceso predeterminada|
|------|------|------|
| SQL Server 2016 |instancia predeterminada|`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`|
| SQL Server 2016 |instancia con nombre |`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES\library`|
| SQL Server de 2017 con R|instancia predeterminada |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` |
| SQL Server de 2017 con R|instancia con nombre|`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` |
| SQL Server de 2017 con Python |instancia predeterminada |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library` |
| SQL Server de 2017 con Python|instancia con nombre|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES\library` |

### <a name="r-server-standalone-or-machine-learning-server-standalone"></a>R Server (independiente) o servidor de aprendizaje de máquina (independiente)

Esta tabla enumeran las rutas de acceso predeterminadas de los archivos binarios cuando se instala el servidor independiente mediante el programa de instalación de SQL Server. 

|Versión| Installation|Ruta de acceso predeterminada|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|Servidor, con R de aprendizaje automático |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|Servidor, con Python de aprendizaje automático |`C:\Program Files\Microsoft SQL Server\130\PYTHON_SERVER`|

Si instala Microsoft R Server o servidor de aprendizaje automático mediante el instalador independiente de Windows, las rutas de acceso son diferentes: por lo general, es algo como `C:\Program Files\Microsoft\R Server\R_SERVER`. Para obtener más información, vea:
 
+ [Instalar para Windows Server de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar a R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="what-is-included-in-a-default-installation"></a>¿Qué se incluye en una instalación predeterminada

En esta sección se proporciona un resumen de las características de R o Python que se instalan de forma predeterminada.

### <a name="default-r-installation-for-sql-server"></a>Instalación predeterminada R para SQL Server

De forma predeterminada la R **base** paquetes instalados. Paquetes base incluyen funcionalidad básica proporcionada por paquetes como `stats` y `utils`.

Una instalación básica de R también incluye numerosos conjuntos de datos de ejemplo y las herramientas estándar de R como RGui (un editor interactivo ligero) y RTerm (una línea de comandos de R).

Instalación de R en SQL Server 2016 o SQL Server 2017 también incluye el **RevoScaleR** paquete y paquetes mejorados relacionados y los proveedores, que es compatible con contextos de proceso remoto, transmisión por secuencias, ejecución de la función rx, en paralelo y muchas otras características.

Para actualizar el paquete RevoScaleR, ya sea utilizar el enlace para actualizar solo los componentes, de aprendizaje de automático o revisiones o actualizar la instancia a una versión más reciente de SQL Server.

+ Para obtener información general de las características mejoradas de R, consulte [sobre el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ Para descargar las bibliotecas de RevoScaleR en un equipo cliente, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

### <a name="default-python-installation-for-sql-server"></a>Instalación de Python para SQL Server predeterminada

Si selecciona los características y la opción de lenguaje de Python de aprendizaje automático, se instala una distribución de Anaconda. La versión exacta depende de la versión de SQL Server ha instalado y si ha actualizado la instancia mediante el instalador del servidor de aprendizaje de máquina.

|Versión| Versión de anaconda| Otros cambios|
|------|------|------|
| RTM de SQL Server de 2017| 3.5.2| Nuevo: revoscalepy|
| actualizar a través del servidor de aprendizaje de máquina 9.2.1 septiembre de 2017| Anaconda 4.2| actualizaciones de revoscalepy |
| SQL Server de 2017 CU3| Anaconda 4.2| actualizaciones de revoscalepy |

Además de las bibliotecas de código de Python, la instalación estándar incluye datos de ejemplo, pruebas unitarias y scripts de ejemplo.

## <a name="restrictions-and-known-issues"></a>Restricciones y problemas conocidos

Puede usar cualquier solución que se ejecuta en SQL Server **sólo** paquetes que están instalados en la biblioteca predeterminada asociada a la instancia.

Si utiliza el enlace para actualizar los componentes de R en una instancia, puede cambiar la ruta de acceso a la biblioteca de la instancia. Asegúrese de comprobar la ruta de acceso de la biblioteca utilizada actualmente por SQL Server.

## <a name="administrative-permissions-required-for-package-installation"></a>Permisos administrativos necesarios para la instalación del paquete

Se cambiaron los permisos necesarios para la instalación del paquete entre SQL Server 2016 y 2017 de SQL Server.

+ En SQL Server 2016, se requiere para la instalación de nuevos paquetes de R acceso administrativo.

+ En SQL Server 2017, aún puede instalar paquetes como un administrador de R y Python y probablemente es el método más fácil.

    La instrucción de DDL, crear biblioteca externa, permite al administrador de base de datos instalar paquetes sin con herramientas de R. 

    Si usa la característica de administración de paquetes en servidor de aprendizaje de máquina, puede usar RevoScaleR para instalar paquetes de R en el nivel de base de datos. El Administrador de base de datos debe habilitar la característica y, a continuación, conceder a los usuarios la capacidad para instalar sus propios paquetes por base de datos. Para obtener más información, consulte [habilitar la administración de paquetes mediante DDL](r-package-how-to-enable-or-disable.md).

### <a name="user-libraries-are-not-supported"></a>No se admiten las bibliotecas de usuario

Los usuarios que no se pueden instalar un paquete en una ubicación protegida a menudo recurren a la instalación de un paquete en una biblioteca de usuario. Sin embargo, esto no es posible en el entorno de SQL Server. Incluso al sistema de archivos está restringido a menudo en el servidor.

Incluso si tiene derechos de administrador y el acceso a una carpeta de documentos de usuario en el servidor, el tiempo de ejecución de script externo que se ejecuta en SQL Server no puede tener acceso a los paquetes instalados fuera de la biblioteca de la instancia predeterminada.

Para obtener sugerencias sobre cómo resolver problemas relacionados con las bibliotecas de usuario, consulte [paquete instalado en las bibliotecas de usuario](packages-installed-in-user-libraries.md).