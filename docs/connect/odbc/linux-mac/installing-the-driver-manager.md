---
title: Instalar el Administrador de controladores (controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cd45cc3b0db61e87c8d9ce506e141cc9ad8c97c5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798788"
---
# <a name="installing-the-driver-manager"></a>Instalación del Administrador de controladores
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo contiene instrucciones para instalar el Administrador de controladores unixODBC para su uso con todas las versiones de Microsoft ODBC Driver for SQL Server en Linux y macOS.  

> [!IMPORTANT]  
> Elimine los paquetes de Administrador de controladores instalados en el equipo antes de instalar el Administrador de controladores unixODBC. La instalación del Administrador de controladores unixODBC podría provocar un error en los Administradores de controladores existentes.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Instalación del Administrador de controladores para Microsoft ODBC Driver 13, 13.1 y 17
La dependencia de administrador de controlador se resuelve automáticamente por el sistema de administración de paquetes cuando se instala Microsoft ODBC Driver 17 for SQL Server en Linux o macOS, 13.1 o 13 siguiendo las instrucciones de [instalar el controlador ODBC de Microsoft para SQL Server en Linux o macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Instalación del Administrador de controladores para Microsoft ODBC Driver 11 for SQL Server  

(Solo Linux Red Hat y SUSE).

**Uso del script de instalación**  
  
> [!IMPORTANT]  
> Estas instrucciones se refieren a `msodbcsql-11.0.2270.0.tar.gz`, que es el archivo de instalación para Red Hat Linux. Si va a instalar la versión preliminar para SUSE Linux, el nombre de archivo es `msodbcsql-11.0.2260.0.tar.gz`.  

Siga estos pasos para instalar el Administrador de controladores:  
  
1.  Asegúrese de que tiene permisos de raíz.  
  
2.  Vaya al directorio donde la descarga de [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC Driver ha colocado el archivo denominado `msodbcsql-11.0.2270.0.tar.gz`. Asegúrese de que dispone del archivo \*.tar.gz que coincida con la versión de Linux. Para extraer los archivos, ejecute el comando siguiente: **tar xvzf msodbcsql-11.0.2270.0.tar.gz**.  

3.  Cambie al directorio `msodbcsql-11.0.2270.0`; allí verá un archivo llamado `build_dm.sh`. Puede ejecutar `build_dm.sh` para instalar el Administrador de controladores unixODBC.

4.  Para ver una lista de las opciones disponibles, ejecute el siguiente comando: **./build_dm.sh --help**.  
  
5.  Cuando esté listo para instalar, y si el equipo puede acceder a un sitio externo a través de FTP, ejecute el siguiente comando: **./build_dm.sh**.

Si el equipo no puede acceder a un sitio externo a través de FTP, obtenga `unixODBC-2.3.0.tar.gz`. Puede obtener `unixODBC-2.3.0.tar.gz` desde [http://www.unixodbc.org](http://www.unixodbc.org/). Haga clic en el vínculo **Descargar** de la parte izquierda de la página para ir a la página de descarga. Después, haga clic en el vínculo correspondiente para descargar unixODBC-2.3.0 (no unixODBC-2.3.1). unixODBC-2.3.1 no es compatible con esta versión de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ejecute el siguiente comando para iniciar la instalación del Administrador de controladores unixODBC: **./build_dm.sh --download-url=file://unixODBC-2.3.0.tar.gz**.  

6.  Escriba **SÍ** para continuar con el desempaquetado de los archivos. Esta parte del proceso puede tardar hasta cinco minutos en completarse.  

7.  Cuando termine de ejecutarse el script, siga las instrucciones que aparecen en la pantalla para instalar el Administrador de controladores unixODBC.

De esta forma, estará preparado para instalar el controlador. Para obtener más información, consulte [instalación Microsoft ODBC Driver for SQL Server en Linux y macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  

**Instalación manual**

Si el script de instalación no se puede completar, configure y compile manualmente el Administrador de controladores adecuado.

1.  Quite cualquier versión anterior instalada de unixODBC (por ejemplo, unixODBC 2.2.11). En Red Hat Enterprise Linux 5 o 6, ejecute el siguiente comando: **yum remove unixODBC**. En SUSE Linux Enterprise, **zypper quitar unixODBC**.  
  
2.  Vaya a [http://www.unixodbc.org](http://www.unixodbc.org/). Haga clic en el vínculo **Descargar** de la parte izquierda de la página para ir a la página de descarga. Después, haga clic en el vínculo correspondiente para guardar el archivo unixODBC-2.3.0.tar.gz en el equipo. UnixODBC-2.3.1 no es compatible con esta versión de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
3.  En el equipo Linux, ejecute el comando: **tar xvzf unixODBC-2.3.0**.  
  
4.  Cambie al directorio unixODBC-2.3.0.  
  
5.  En un símbolo del sistema, ejecute el comando: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8"** .  
  
6.  En un símbolo del sistema, ejecute el comando: **export CPPFLAGS**.  
  
7.  En un símbolo del sistema, ejecute el comando: **"./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE"** .  
  
8.  En un símbolo del sistema (con una sesión iniciada con permisos de raíz), ejecute el comando: **make**.  
  
9. En un símbolo del sistema (con una sesión iniciada con permisos de raíz), ejecute el comando: **make install**.  

De esta forma, estará preparado para instalar el controlador. Para obtener más información, consulte [instalación Microsoft ODBC Driver for SQL Server en Linux y macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  
  
## <a name="see-also"></a>Ver también
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
