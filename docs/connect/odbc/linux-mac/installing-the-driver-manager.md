---
title: Instalar el Administrador de controladores (controlador ODBC para SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e465c3fa67375316be9cfbe614dfd5bfa62b7823
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="installing-the-driver-manager"></a>Instalación del Administrador de controladores
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artículo contiene instrucciones para instalar el Administrador de controladores unixODBC para su uso con todas las versiones de Microsoft ODBC Driver for SQL Server en Linux y macOS.  

> [!IMPORTANT]  
> Elimine los paquetes de Administrador de controladores instalados en el equipo antes de instalar el Administrador de controladores unixODBC. La instalación del Administrador de controladores unixODBC podría provocar un error en los Administradores de controladores existentes.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Instalar al administrador de controladores de Microsoft ODBC Driver 13, 13.1 y 17
La dependencia de administrador de controladores se resuelve automáticamente por el sistema de administración de paquetes cuando se instala Microsoft ODBC Driver 13, 13.1 o 17 para SQL Server en Linux o Mac OS siguiendo las instrucciones de [instalar el controlador ODBC de Microsoft para SQL Server en Linux o Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Instalación del Administrador de controladores para Microsoft ODBC Driver 11 for SQL Server  

(SUSE y Red Hat Linux solo).

**Uso de la secuencia de comandos de instalación**  
  
> [!IMPORTANT]  
> Estas instrucciones hacen referencia a `msodbcsql-11.0.2270.0.tar.gz`, que es el archivo de instalación para Red Hat Linux. Si va a instalar la versión preliminar para SUSE Linux, el nombre de archivo es `msodbcsql-11.0.2260.0.tar.gz`.  

Siga estos pasos para instalar el Administrador de controladores:  
  
1.  Asegúrese de que tiene permisos de raíz.  
  
2.  Vaya al directorio donde el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] descarga de ODBC Driver colocó el archivo denominado `msodbcsql-11.0.2270.0.tar.gz`. Asegúrese de que dispone del archivo \*.tar.gz que coincida con la versión de Linux. Para extraer los archivos, ejecute el siguiente comando: **tar xvzf msodbcsql-11.0.2270.0**.  

3.  Cambie a la `msodbcsql-11.0.2270.0` directorio y allí verá un archivo denominado `build_dm.sh`. Puede ejecutar `build_dm.sh` para instalar el Administrador de controladores unixODBC.

4.  Para ver una lista de las opciones disponibles, ejecute el siguiente comando: **./build_dm.sh--ayuda**.  
  
5.  Cuando esté listo para instalar, y si el equipo puede tener acceso a un sitio externo a través de FTP, ejecute el siguiente comando: **./build_dm.sh**.

Si el equipo no puede obtener acceso a un sitio externo a través de FTP, obtener `unixODBC-2.3.0.tar.gz`. Puede obtener `unixODBC-2.3.0.tar.gz` de [ http://www.unixodbc.org ](http://www.unixodbc.org/). Haga clic en el **descargar** vínculo en el lado izquierdo de la página para ir a la página de descarga. Después, haga clic en el vínculo correspondiente para descargar unixODBC-2.3.0 (no unixODBC-2.3.1). UnixODBC-2.3.1 no es compatible con esta versión de la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Ejecute el siguiente comando para iniciar la instalación del Administrador de controladores unixODBC: **./build_dm.sh--dirección url de descarga = file://unixODBC-2.3.0.tar.gz**.  

6.  Tipo de **Sí** para continuar con el desempaquetado de los archivos. Esta parte del proceso puede tardar hasta cinco minutos en completarse.  

7.  Cuando termine de ejecutarse el script, siga las instrucciones que aparecen en la pantalla para instalar el Administrador de controladores unixODBC.

De esta forma, estará preparado para instalar el controlador. Para obtener más información, consulte [instalar Microsoft ODBC Driver for SQL Server en Linux y Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  

**Instalación manual**

Si el script de instalación no se puede completar, configure y compile manualmente el Administrador de controladores adecuado.

1.  Quite cualquier versión anterior instalada de unixODBC (por ejemplo, unixODBC 2.2.11). En Red Hat Enterprise Linux 5 o 6, ejecute el siguiente comando: **yum quitar unixODBC**. En SUSE Linux Enterprise, **zypper quitar unixODBC**.  
  
2.  Vaya a [ http://www.unixodbc.org ](http://www.unixodbc.org/). Haga clic en el **descargar** vínculo en el lado izquierdo de la página para ir a la página de descarga. Después, haga clic en el vínculo correspondiente para guardar el archivo unixODBC-2.3.0.tar.gz en el equipo. UnixODBC-2.3.1 no es compatible con esta versión de la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
3.  En el equipo Linux, ejecute el comando: **tar xvzf unixODBC-2.3.0**.  
  
4.  Cambie al directorio unixODBC-2.3.0.  
  
5.  En un símbolo del sistema, ejecute el comando: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8"**.  
  
6.  En un símbolo del sistema, ejecute el comando: **exportar CPPFLAGS**.  
  
7.  En un símbolo del sistema, ejecute el comando: **". / configurar--prefix = / usr--libdir = / usr/lib64--sysconfdir = / etcetera--habilitar gui = n--habilitar controladores = n--enable-iconv--con-iconv-char-enc = UTF8--con-iconv-ucode-enc = UTF16LE"**.  
  
8.  En un símbolo del sistema (iniciado sesión como raíz), ejecute el comando: **realizar**.  
  
9. En un símbolo del sistema (iniciado sesión como raíz), ejecute el comando: **Asegúrese de instalar**.  

De esta forma, estará preparado para instalar el controlador. Para obtener más información, consulte [instalar Microsoft ODBC Driver for SQL Server en Linux y Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  
  
## <a name="see-also"></a>Vea también
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)
