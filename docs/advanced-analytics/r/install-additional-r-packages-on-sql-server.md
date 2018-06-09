---
title: Instalar nuevos paquetes de R en SQL Server Machine Learning Services | Documentos de Microsoft
description: Agregar nuevos paquetes de R para SQL Server 2016 R Services o SQL Server de 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e05842a8e8a5a1d2454dbbe500b4d5aa95fca660
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707083"
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar nuevos paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server donde está habilitado el aprendizaje automático. Existen varios métodos para instalar nuevos paquetes de R, dependiendo de qué versión de SQL Server tiene, y si el servidor tiene una conexión a internet. Los métodos siguientes para la nueva instalación de paquete son posibles.

| Método                           | Permisos               | Remota o Local |
|------------------------------------|---------------------------|--------------|
| [Utilizar administradores de paquetes de R convencionales](use-r-package-managers-on-sql-server.md)  | Administración | Local |
| [Uso de RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Habilitadas para administración, después los roles de base de datos | both|
| [Usar T-SQL (crear biblioteca externa)](install-r-packages-tsql.md) | Habilitadas para administración, después los roles de base de datos | both 

## <a name="who-installs-permissions"></a>Que instala (permisos)

La biblioteca de paquetes de R se encuentra físicamente en la carpeta archivos de programa de su instancia de SQL Server, en una carpeta segura con acceso restringido. En la escritura en esta ubicación se requiere permisos de administrador.

No administradores pueden instalar paquetes, pero para ello se requiere configuración de addititional y funcionalidad no está disponible en las instalaciones iniciales. Existen dos enfoques para las instalaciones del paquete sin derechos administrativos: RevoScaleR usando versión 9.0.1 y versiones posteriores, o bien usar crear biblioteca externa (solo SQL Server 2017). En SQL Server de 2017 **dbo_owner** o de otro usuario con permiso de crear una biblioteca externa puede instalar paquetes de R en la base de datos actual.

Los desarrolladores de R están acostumbrados a crear bibliotecas de usuario para los paquetes que necesitan si bibliotecas ubicadas centralmente están off-limits. Esta práctica es problemática para código de R que se ejecuta en una instancia del motor de base de datos de SQL Server. SQL Server no se puede cargar paquetes desde bibliotecas externas, incluso si dicha biblioteca está en el mismo equipo. Solo los paquetes de la biblioteca de la instancia pueden usarse en código de R que se ejecuta en SQL Server.

Normalmente tiene restringido el acceso al sistema de archivos en el servidor e incluso si tiene derechos de administrador y el acceso a una carpeta de documentos de usuario en el servidor, el tiempo de ejecución de script externo que se ejecuta en SQL Server no puede tener acceso a los paquetes instalados fuera de la instancia predeterminada biblioteca. 

## <a name="considerations-for-package-installation"></a>Consideraciones para la instalación del paquete

Antes de instalar nuevos paquetes, considere la posibilidad de si las capacidades habilitadas por un determinado paquete son adecuadas en un entorno de SQL Server. En un entorno de SQL Server protegido, puede evitar lo siguiente:

+ Paquetes que requieren acceso a la red
+ Paquetes que requieren Java u otros marcos de trabajo no se suele usados en un entorno de SQL Server
+ Paquetes que requieren acceso al sistema de archivos con privilegios elevados
+ Paquete se utiliza para desarrollo web y otras tareas que no se benefician al ejecutarse dentro de SQL Server

## <a name="offline-installation-no-internet-access"></a>Instalación sin conexión (sin acceso a internet)

En general, los servidores que hospedan las bases de datos de producción bloquear las conexiones de internet. Instalar nuevos paquetes de R o Python en dichos entornos requiere que preparar los paquetes y dependencias de antemano y copie los archivos en una carpeta en el servidor para la instalación sin conexión.

Identificar todas las dependencias será complicada. Para R, recomendamos que use [miniCRAN para crear un repositorio local](create-a-local-package-repository-using-minicran.md) y, a continuación, transfiera el repositorio definido por completo a una instancia de SQL Server aislada.

Alternativley, puede realizar este paso manualmente:

1. Identificar todas las dependencias del paquete. 
2. Compruebe si los paquetes necesarios ya están instalados en el servidor. Si el paquete está instalado, compruebe que la versión es correcta.
3. Descargue el paquete y todas las dependencias en un equipo independiente.
4. Mover los archivos a una carpeta accesible por el servidor.
5. Ejecutar un comando de instalación compatible o la instrucción DDL para instalar el paquete en la biblioteca de la instancia.

### <a name="download-the-package-as-a-zipped-file"></a>Descargar el paquete como un archivo comprimido

Para la instalación en un servidor sin acceso a internet, debe descargar una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. **Descomprima el paquete.**

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta de la [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) paquete desde Bioconductor, suponiendo que el equipo tiene acceso a internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic en el vínculo a la. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **guardar**.

    Este proceso crea una copia local del paquete. 

4. Si recibe un error de descarga, pruebe a un sitio de réplica diferente.

5. Después de que se ha descargado el archivo de paquete, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a internet.

> [!TIP]
> Si por error instala el paquete en lugar de descargar los archivos binarios, también se guarda una copia del archivo zip descargado en el equipo. Ver los mensajes de estado tal y como se instala el paquete para determinar la ubicación del archivo. Puede copiar dicho archivo comprimido en el servidor que no tiene acceso a internet.
> 
> Sin embargo, al obtener paquetes con este método, no se incluyen las dependencias. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalación en paralelo con Standalone R o servidores de Python

Funciones de R y Python se incluyen en varios productos de Microsoft, todos los cuales pueden coexistir en el mismo equipo.

Si ha instalado SQL Server 2017 Microsoft máquina aprendizaje Server (independiente) o SQL Server 2016 R Server (independiente) además de los análisis en bases de datos (SQL Server 2017 Machine Learning Services y SQL Server 2016 R Services), el equipo tiene independiente instalaciones de R para cada una, con los duplicados de todas las bibliotecas y herramientas de R.

Paquetes que se instalan en la biblioteca R_SERVER solo son utilizados por un servidor independiente y no se pueden tener acceso a una instancia de SQL Server (In-Database). Utilice siempre el `R_SERVICES` biblioteca al instalar los paquetes que desea utilizar en bases de datos en SQL Server. Para obtener más información acerca de las rutas de acceso, consulte [ubicación de biblioteca del paquete](installing-and-managing-r-packages.md#package-library-location).


## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)