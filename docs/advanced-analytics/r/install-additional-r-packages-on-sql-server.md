---
title: Instalar nuevos paquetes de idioma de R
description: Agregar nuevos paquetes de R a SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (in-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8de02f679af1bbeed8f65f4e4dc5456cd414e75e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345545"
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar nuevos paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R en una instancia de SQL Server en la que está habilitado el aprendizaje automático. Hay varios métodos para instalar nuevos paquetes de R, en función de la versión de SQL Server que tenga y de si el servidor tiene una conexión a Internet. Se pueden realizar los siguientes enfoques para la instalación de nuevos paquetes.

| Método                           | Permisos               | Remoto/local |
|------------------------------------|---------------------------|--------------|
| [Usar administradores de paquetes de R convencionales](use-r-package-managers-on-sql-server.md)  | Administración | Local |
| [Uso de RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Habilitado para administradores y roles de base de datos después | both|
| [Usar T-SQL (crear biblioteca externa)](install-r-packages-tsql.md) | Habilitado para administradores y roles de base de datos después | both 

## <a name="who-installs-permissions"></a>Quién instala (permisos)

La biblioteca de paquetes de R se encuentra físicamente en la carpeta archivos de programa de la instancia de SQL Server, en una carpeta segura con acceso restringido. La escritura en esta ubicación requiere permisos de administrador.

Los usuarios que no son administradores pueden instalar paquetes, pero esto requiere una configuración adicional y la capacidad no está disponible en las instalaciones iniciales. Existen dos enfoques para las instalaciones de paquetes que no son de administrador: RevoScaleR con la versión 9.0.1 y versiones posteriores, o el uso de CREATE EXTERNAL LIBRARY (solo SQL Server 2017). En SQL Server 2017, **dbo_owner** u otro usuario con permiso CREATE external library puede instalar paquetes de R en la base de datos actual.

Los desarrolladores de R están acostumbrados a crear bibliotecas de usuario para los paquetes que necesitan si las bibliotecas ubicadas de forma centralizada están fuera de los límites. Esta práctica es problemática para el código de R que se ejecuta en una instancia del motor de base de datos de SQL Server. SQL Server no puede cargar paquetes de bibliotecas externas, aunque la biblioteca esté en el mismo equipo. Solo los paquetes de la biblioteca de instancias se pueden usar en el código de R que se ejecuta en SQL Server.

El acceso al sistema de archivos suele estar restringido en el servidor e incluso si tiene derechos de administrador y tiene acceso a una carpeta de documentos de usuario en el servidor, el tiempo de ejecución de script externo que se ejecuta en SQL Server no puede tener acceso a los paquetes instalados fuera de la instancia predeterminada. Biblioteca. 

## <a name="considerations-for-package-installation"></a>Consideraciones para la instalación de paquetes

Antes de instalar nuevos paquetes, tenga en cuenta si las capacidades habilitadas por un paquete determinado son adecuadas en un entorno de SQL Server. En un entorno de SQL Server protegido, puede que desee evitar lo siguiente:

+ Paquetes que requieren acceso a la red
+ Paquetes que requieren acceso al sistema de archivos elevado
+ El paquete se usa para el desarrollo web u otras tareas que no se beneficien al ejecutarse dentro de SQL Server

## <a name="offline-installation-no-internet-access"></a>Instalación sin conexión (sin acceso a Internet)

En general, los servidores que hospedan bases de datos de producción bloquean las conexiones a Internet. La instalación de nuevos paquetes de R o Python en estos entornos requiere preparar los paquetes y las dependencias de antemano y copiar los archivos en una carpeta en el servidor para la instalación sin conexión.

La identificación de todas las dependencias resulta complicada. Para R, se recomienda usar [miniCRAN para crear un repositorio local](create-a-local-package-repository-using-minicran.md) y, a continuación, transferir el repositorio totalmente definido a una instancia de SQL Server aislada.

Como alternativa, puede realizar estos pasos manualmente:

1. Identifique todas las dependencias de paquete. 
2. Compruebe si los paquetes necesarios ya están instalados en el servidor. Si el paquete está instalado, compruebe que la versión es correcta.
3. Descargue el paquete y todas las dependencias en un equipo independiente.
4. Mueva los archivos a una carpeta a la que tenga acceso el servidor.
5. Ejecute un comando de instalación compatible o una instrucción DDL para instalar el paquete en la biblioteca de instancias.

### <a name="download-the-package-as-a-zipped-file"></a>Descargar el paquete como un archivo comprimido

Para instalar en un servidor sin acceso a Internet, debe descargar una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. **No descomprima el paquete.**

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta del paquete [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) de Bioconductor, suponiendo que el equipo tenga acceso a Internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic con el botón secundario en el vínculo al. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **Guardar**.

    Este proceso crea una copia local del paquete. 

4. Si recibe un error de descarga, pruebe con otro sitio reflejado.

5. Una vez descargado el archivo de paquete, puede instalar el paquete o copiar el paquete comprimido en un servidor que no tenga acceso a Internet.

> [!TIP]
> Si, por error, instala el paquete en lugar de descargar los archivos binarios, también se guarda una copia del archivo comprimido descargado en el equipo. Vea los mensajes de estado como el paquete está instalado para determinar la ubicación del archivo. Puede copiar ese archivo comprimido en el servidor que no tiene acceso a Internet.
> 
> Sin embargo, al obtener paquetes con este método, no se incluyen las dependencias. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalación en paralelo con servidores R o Python independientes

Las características de R y Python se incluyen en varios productos de Microsoft, que pueden coexistir en el mismo equipo.

Si instaló SQL Server 2017 Microsoft Machine Learning Server (independiente) o SQL Server 2016 R Server (independiente) además de análisis en base de datos (SQL Server 2017 Machine Learning Services y SQL Server 2016 R Services), el equipo tiene instalaciones de R para cada, con duplicados de todas las herramientas y bibliotecas de R.

Los paquetes que se instalan en la biblioteca R_SERVER solo se usan en un servidor independiente y no se puede tener acceso a ellos mediante una instancia de SQL Server (en la base de datos). Use siempre la `R_SERVICES` biblioteca al instalar los paquetes que desea utilizar en la base de datos en SQL Server. Para obtener más información sobre las rutas de acceso, vea ubicación de la [biblioteca de paquetes](../package-management/default-packages.md).

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)
