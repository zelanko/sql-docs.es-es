---
title: Instalar y administrar paquetes de aprendizaje de máquina en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cbab4687dd0d5a8cb250fa38fc4c4c7dbb9d68a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="install-and-manage-machine-learning-packages-in-sql-server"></a>Instalar y administrar paquetes de aprendizaje de máquina en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo puede instalar nuevos paquetes de R o Python en 2017 de SQL Server y en SQL Server 2016. También describe las limitaciones en los paquetes que se pueden instalar en SQL Server.

## <a name="overview-of-package-management-methods-and-requirements"></a>Información general sobre los métodos de administración de paquetes y los requisitos

A diferencia de un desarrollo típicas de R o Python, paquetes utilizados por SQL Server deben instalarse en una carpeta bajo el control administrativo. Hay numerosas ventajas para mantener los paquetes en una sola ubicación:

+ El administrador del servidor puede supervisar la adición de nuevos archivos y bibliotecas en el servidor y controlar el crecimiento de archivos utilizados por las bibliotecas de paquete. 
+ Los paquetes se pueden compartir con mayor facilidad por varios usuarios de base de datos, en lugar de instalar varias copias del mismo paquete en bibliotecas de usuario.
+ Solo los paquetes protegidos, aprobados pueden instalarse, para proteger el servidor y sus operaciones.

Sin embargo, estas restricciones necesariamente algunos cambios en la manera en que los científicos de datos y los analistas de trabajo:

+ Normalmente, el acceso administrativo al servidor es necesario. En SQL Server 2017, el Administrador de base de datos puede usar roles para conceder a determinados usuarios la capacidad para instalar paquetes de uso privado, pero todavía, el administrador debe habilitar esta característica.
+ Muchos servidores no tienen acceso a Internet. Instalación de paquetes en estos equipos, requiere una preparación adicional.
+ Los paquetes se instalan en una biblioteca de la instancia. Los paquetes no se pueden compartir entre instancias.
+ Los usuarios no pueden ejecutar cualquier paquete que se ha instalado en una biblioteca de usuario.

## <a name="package-installation-guides-for-r-or-python"></a>Guías de instalación de paquete de R o Python

Consulte los artículos siguientes para obtener instrucciones detalladas sobre cómo instalar nuevos paquetes de R o Python. 

### <a name="install-new-r-packages"></a>Instalar nuevos paquetes de R

+ [Instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md)

    Puede instalar paquetes de R en SQL Server 2016 o 2017 como administrador, con herramientas de R.

    También puede instalar paquetes de R desde un cliente remoto de R donde R Server 9.0.2 o una versión posterior está instalado.

    También puede instalar paquetes de R en SQL Server 2017 mediante instrucciones de DDL.

### <a name="install-new-python-packages"></a>Instalar nuevos paquetes de Python

+ [Instalación de paquetes de Python adicionales en SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="prerequisites"></a>Requisitos previos

Antes de intentar descargar o instalar cualquier paquete de nuevo, revise los requisitos:

+ Asegúrese de que hay una versión de Windows del paquete: [obtener la versión de paquete correcto y formato](#packageVersion)

+ Identificar todas las dependencias de paquete y determinar su compatibilidad con el entorno de SQL Server.

+ Compruebe la versión de R o compatibilidad de versiones de Python. El paquete debe ser compatible con la versión de R o Python que se ejecuta en SQL Server.

+ Permisos. Determine si tiene derechos para instalar el paquete. Para instalar en la biblioteca de instancia, se requiere acceso administrativo al equipo que ejecuta SQL Server. Si no tiene acceso administrativo al equipo de SQL Server, busque un administrador de base de datos para ayudar con la instalación del paquete.

    En SQL Server 2017, puede instalar paquetes de R desde un cliente remoto, si se ha habilitado la administración de paquetes en el servidor y es propietario de la base de datos o un miembro de un rol de administración del paquete.

+ Tenga en cuenta los riesgos y los beneficios de la instalación de un paquete determinado en el entorno de SQL Server. Comprobar si el paquete (o todos los paquetes que requiere) contienen características que se bloquearía por SQL Server o por la directiva. Muchos paquetes de R y Python son una opción muy deficiente para un entorno de SQL Server protegido. Problemas podrían incluir:

    - Paquetes que tienen acceso a la red
    - Paquetes que requieren Java u otros marcos de trabajo no se suele usados en un entorno de SQL Server
    - Paquetes que requieren acceso al sistema de archivos con privilegios elevados
    - Paquete se utiliza para desarrollo web y otras tareas que no se benefician al ejecutarse dentro de SQL Server.

## <a name="installation-on-servers-with-no-internet-access"></a>Instalación en servidores sin acceso a Internet

En general, los servidores que hospedan las bases de datos de producción no permiten la conexión a Internet. Instalar nuevos paquetes de R o Python en dichos entornos requiere que preparar todos los paquetes y sus dependencias de antemano y copie los archivos en una carpeta en el servidor para usarla en la instalación.

1. Identificar todas las dependencias del paquete. 
2. Compruebe si los paquetes necesarios ya están instalados en el servidor. Si el paquete está instalado, compruebe que la versión es correcta.
3. Descargue el paquete y todas las dependencias en un equipo independiente.
4. Mover los archivos a una carpeta accesible por el servidor.
5. Ejecutar un comando de instalación compatible o la instrucción DDL para instalar el paquete en la biblioteca de la instancia.

Identificar todas las dependencias puede resultar complicado. Para R, recomendamos que use [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar un repositorio de paquetes sin conexión.

De forma similar para Python, debe preparar todas las dependencias y guardarlos localmente. Asegúrese de usar un archivos binarios de compatible con Windows y use el formato WHL.
