---
title: Instalar nuevos paquetes de idioma R - SQL Server Machine Learning Services
description: Agregar nuevos paquetes de R a SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f443113222181f0909bd72048e3c3f5c739df4ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506926"
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar nuevos paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server que está habilitado el aprendizaje automático. Existen varios métodos para instalar nuevos paquetes de R, dependiendo de qué versión de SQL Server tiene y si el servidor tiene una conexión a internet. Son posibles los siguientes enfoques para la nueva instalación del paquete.

| Método                           | Permisos               | Remota o Local |
|------------------------------------|---------------------------|--------------|
| [Usar los administradores de paquetes de R convencionales](use-r-package-managers-on-sql-server.md)  | Administración | Local |
| [Uso de RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Administrador habilitado, después los roles de base de datos | both|
| [Usar Transact-SQL (crear biblioteca externa)](install-r-packages-tsql.md) | Administrador habilitado, después los roles de base de datos | both 

## <a name="who-installs-permissions"></a>Que instala (permisos)

La biblioteca de paquetes de R se encuentra físicamente en la carpeta archivos de programa de la instancia de SQL Server en una carpeta segura con acceso restringido. Escritura en esta ubicación requiere permisos de administrador.

No administradores pueden instalar paquetes, pero para ello se requiere configuración addititional y funcionalidad no está disponible en las instalaciones iniciales. Hay dos enfoques para las instalaciones de paquetes sin derechos administrativos: RevoScaleR con versión 9.0.1 y versiones posteriores, o mediante CREATE EXTERNAL LIBRARY (sólo en SQL Server 2017). En SQL Server 2017, **dbo_owner** o de otro usuario con permiso CREATE EXTERNAL LIBRARY puede instalar paquetes de R a la base de datos actual.

Los desarrolladores de R están acostumbrados a la creación de bibliotecas de usuario para los paquetes que necesitan si ubicadas centralmente las bibliotecas son navegadores. Esta práctica es problemática para código de R que se ejecuta en una instancia del motor de base de datos de SQL Server. SQL Server no se puede cargar paquetes desde bibliotecas externas, incluso si dicha biblioteca está en el mismo equipo. Solo los paquetes de la biblioteca de instancia se pueden usar en código de R que se ejecuta en SQL Server.

Normalmente se restringe el acceso al sistema de archivos en el servidor y, aunque tenga derechos de administrador y el acceso a una carpeta de documentos de usuario en el servidor, el tiempo de ejecución de scripts externos que se ejecuta en SQL Server no puede tener acceso a los paquetes instalados fuera de la instancia predeterminada biblioteca. 

## <a name="considerations-for-package-installation"></a>Consideraciones para la instalación del paquete

Antes de instalar nuevos paquetes, considere la posibilidad de si las funciones habilitadas por un paquete determinado son adecuadas en un entorno de SQL Server. En un entorno protegido de SQL Server, es posible que desea evitar lo siguiente:

+ Paquetes que requieren acceso a la red
+ Paquetes que requieren Java u otros marcos de trabajo no se suele usados en un entorno de SQL Server
+ Paquetes que requieren acceso al sistema de archivos con privilegios elevados
+ Paquete se utiliza para el desarrollo web y otras tareas que no se benefician mediante la ejecución dentro de SQL Server

## <a name="offline-installation-no-internet-access"></a>Instalación sin conexión (sin acceso a internet)

En general, los servidores que hospedan las bases de datos de producción bloquean conexiones a internet. Instalar nuevos paquetes de R o Python en dichos entornos requiere que preparar los paquetes y dependencias de antemano y copie los archivos en una carpeta en el servidor para la instalación sin conexión.

Identificar todas las dependencias se complica. Para R, recomendamos que use [miniCRAN para crear un repositorio local](create-a-local-package-repository-using-minicran.md) y, a continuación, transferir el repositorio totalmente definido a una instancia aislada de SQL Server.

Alternativley, puede realizar este paso manualmente:

1. Identifique todas las dependencias de paquete. 
2. Compruebe si los paquetes necesarios ya están instalados en el servidor. Si está instalado el paquete, compruebe que la versión es correcta.
3. Descargue el paquete y todas las dependencias en un equipo independiente.
4. Mueva los archivos en una carpeta accesible por el servidor.
5. Ejecutar un comando de instalación admitidos o la instrucción DDL para instalar el paquete en la biblioteca de la instancia.

### <a name="download-the-package-as-a-zipped-file"></a>Descargue el paquete como un archivo comprimido

Para la instalación en un servidor sin acceso a internet, debe descargar una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. **Descomprima el paquete.**

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta de la [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) paquete desde Bioconductor, suponiendo que el equipo tiene acceso a internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic en el vínculo a la. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **guardar**.

    Este proceso crea una copia local del paquete. 

4. Si se produce un error de descarga, pruebe un sitio de réplica diferente.

5. Después de que se ha descargado el archivo de paquete, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a internet.

> [!TIP]
> Si por error instala el paquete en lugar de descargar los archivos binarios, también se guarda una copia del archivo zip descargado en el equipo. Observe los mensajes de estado mientras se instala el paquete para determinar la ubicación del archivo. Puede copiar ese archivo comprimido en el servidor que no tiene acceso a internet.
> 
> Sin embargo, al obtener paquetes mediante este método, no se incluyen las dependencias. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalación en paralelo con Standalone R o Python servidores

Se incluyen las características de R y Python en varios productos de Microsoft, que puede coexistir en el mismo equipo.

Si ha instalado SQL Server 2017 Microsoft Machine Learning Server (independiente) o SQL Server 2016 R Server (independiente) además de los análisis en bases de datos (SQL Server 2017 Machine Learning Services y SQL Server 2016 R Services), el equipo tiene independiente instalaciones de R para cada uno, con los duplicados de todas las bibliotecas y herramientas de R.

Los paquetes que están instalados en la biblioteca R_SERVER solo se usan un servidor independiente y no se pueden tener acceso a una instancia de SQL Server (In-Database). Use siempre la `R_SERVICES` biblioteca al instalar los paquetes que desea usar en bases de datos en SQL Server. Para obtener más información acerca de las rutas de acceso, consulte [ubicación de la biblioteca del paquete](installing-and-managing-r-packages.md#package-library-location).


## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)