---
title: Seguimiento de acceso de datos con el controlador ODBC en Linux y macOS | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
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
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91601184666926fae02ab9c1093bb1898d0515ff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Seguimiento de acceso de datos con el controlador ODBC en Linux y Mac OS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El Administrador de controladores unixODBC en Mac OS y Linux es compatible con el seguimiento de entrada de la llamada de API de ODBC y de salida de ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].

Para realizar el seguimiento de comportamiento de la aplicación ODBC, editar la `odbcinst.ini` del archivo `[ODBC]` sección para establecer los valores `Trace=Yes` y `TraceFile` a la ruta de acceso del archivo que va a contener el seguimiento de salida; por ejemplo:

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(También puede utilizar `/dev/stdout` o cualquier otro nombre de dispositivo para enviar la salida no existe en lugar de un archivo permanente de seguimiento.) Con la configuración anterior, cada vez que una aplicación carga el Administrador de controladores unixODBC registrará todas las llamadas de API de ODBC que realizan en el archivo de salida.

Cuando termine de seguimiento de la aplicación, quite `Trace=Yes` desde el `odbcinst.ini` de archivos para evitar la reducción del rendimiento de la traza y asegúrese de quitan los archivos de seguimiento innecesarios.
  
El seguimiento se aplica a todas las aplicaciones que usan el controlador en `odbcinst.ini`. Para realizar el seguimiento no todas las aplicaciones (por ejemplo, para evitar la divulgación de información confidencial por usuario), puede realizar un seguimiento una instancia de aplicación individual indicando la ubicación de una privada `odbcinst.ini`, usando la `ODBCSYSINI` variable de entorno. Por ejemplo:  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
En este caso, puede agregar `Trace=Yes` a la `[ODBC Driver 13 for SQL Server]` sección de `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinar qué archivo odbc.ini que está usando el controlador

Los controladores ODBC de Linux y Mac OS no sabe en cuál `odbc.ini` está en uso o la ruta de acceso a la `odbc.ini` archivo. Sin embargo, obtener información acerca de qué `odbc.ini` archivo está en uso está disponible en las herramientas de unixODBC `odbc_config` y `odbcinst`y de la documentación del Administrador de controladores unixODBC.  
  
Por ejemplo, el siguiente comando imprime (entre otros datos) la ubicación del sistema y usuario `odbc.ini` archivos que contienen, respectivamente, los DSN de usuario y del sistema:

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

El [documentación de unixODBC](http://www.unixodbc.org/doc/UserManual/) se explican las diferencias entre usuario y DSN del sistema. En resumen:  

- DSN de usuario---se trata de DSN que solo está disponibles para un usuario específico. Los usuarios pueden conectarse mediante, agregar, modificar y quitar su propios DSN de usuario. DSN de usuario se almacenan en un archivo en el directorio principal del usuario o un subdirectorio del mismo.
  
- DSN de sistema---estos DSN están disponibles para todos los usuarios en el sistema para conectarse con ellos, pero pueden solo agregar, modificar y quitar un administrador del sistema. Si un usuario tiene un DSN de usuario con el mismo nombre que un DSN de sistema, el DSN de usuario se usarán en conexiones por usuario.

## <a name="see-also"></a>Vea también
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
