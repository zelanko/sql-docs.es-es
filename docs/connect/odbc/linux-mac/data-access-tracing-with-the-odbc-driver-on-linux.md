---
title: Seguimiento de acceso a datos con el controlador ODBC en Linux y macOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ad5d49841db9abdd0b512c1d36454eccc5ff73a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782883"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Seguimiento de acceso a datos con el controlador ODBC en Linux y macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El Administrador de controladores unixODBC en macOS y Linux es compatible con el seguimiento de entrada de la llamada de API de ODBC y salir del controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Para realizar un seguimiento ODBC comportamiento de su aplicación, edite el `odbcinst.ini` del archivo `[ODBC]` sección para establecer los valores `Trace=Yes` y `TraceFile` a la ruta de acceso del archivo que va a contener el seguimiento de la salida; por ejemplo:

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(También puede usar `/dev/stdout` o cualquier otro nombre de dispositivo para enviar la salida no existe en lugar de a un archivo persistente del seguimiento.) Con la configuración anterior, cada vez que una aplicación carga el Administrador de controladores unixODBC, registrará todas las llamadas de API de ODBC que realizan en el archivo de salida.

Cuando termine de seguimiento de la aplicación, quite `Trace=Yes` desde el `odbcinst.ini` para evitar la disminución del rendimiento de seguimiento de archivos y asegúrese de quitan los archivos de seguimiento innecesarios.
  
El seguimiento se aplica a todas las aplicaciones que utilizan el controlador de `odbcinst.ini`. Para no realizar el seguimiento de todas las aplicaciones (por ejemplo, para evitar la divulgación de información confidencial de los usuarios), puede llevar a cabo este proceso en una instancia de aplicación individual indicando la ubicación de un archivo `odbcinst.ini` privado mediante la variable de entorno `ODBCSYSINI`. Por ejemplo:  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
En este caso, puede agregar `Trace=Yes` a la `[ODBC Driver 13 for SQL Server]` sección de `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinación del archivo ODBC.ini que está utilizando el controlador

Los controladores ODBC de Linux y macOS no sabe en cuál `odbc.ini` está en uso o la ruta de acceso a la `odbc.ini` archivo. Sin embargo, la información sobre qué `odbc.ini` archivo está en uso está disponible en las herramientas de unixODBC `odbc_config` y `odbcinst`y de la documentación del Administrador de controladores unixODBC.  
  
Por ejemplo, el siguiente comando imprime (entre otros datos) la ubicación de los archivos `odbc.ini` de los usuarios y del sistema que contienen, respectivamente, los DSN de usuario y sistema:

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

El [documentación de unixODBC](http://www.unixodbc.org/doc/UserManual/) se explican las diferencias entre usuario y los DSN del sistema. En resumen:  

- DSN de usuario---estos son los DSN que solo están disponibles para un usuario específico. Los usuarios pueden conectarse mediante, agregar, modificar y quitar su propios DSN de usuario. DSN de usuario se almacenan en un archivo en el directorio principal del usuario o un subdirectorio del mismo.
  
- Los DSN del sistema---estos DSN están disponibles para todos los usuarios en el sistema para conectarse con ellos, pero pueden solo se agregado, modificados y quitar un administrador del sistema. Si un usuario tiene un DSN de usuario con el mismo nombre que un DSN de sistema, el DSN de usuario se usarán en conexiones por usuario.

## <a name="see-also"></a>Ver también
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
