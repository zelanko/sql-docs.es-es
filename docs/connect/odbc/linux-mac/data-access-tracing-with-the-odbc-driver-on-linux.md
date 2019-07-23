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
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008821"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Seguimiento de acceso a datos con el controlador ODBC en Linux y macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El administrador de controladores unixODBC en macOS y Linux admite el seguimiento de la entrada de llamada de la API de ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]y la salida del controlador ODBC para.

Para realizar un seguimiento del comportamiento de ODBC de la `odbcinst.ini` aplicación, `[ODBC]` edite la sección del `Trace=Yes` archivo `TraceFile` para establecer los valores y en la ruta de acceso del archivo que va a contener el resultado del seguimiento; por ejemplo:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(También puede usar `/dev/stdout` o cualquier otro nombre de dispositivo para enviar la salida del seguimiento en lugar de a un archivo persistente). Con la configuración anterior, cada vez que una aplicación carga el administrador de controladores unixODBC, registrará todas las llamadas a la API de ODBC que haya realizado en el archivo de salida.

Después de finalizar el seguimiento de la aplicación `Trace=Yes` , quite `odbcinst.ini` del archivo para evitar la reducción del rendimiento del seguimiento y asegúrese de que se quitan los archivos de seguimiento innecesarios.

El seguimiento se aplica a todas las aplicaciones que utilizan el controlador de `odbcinst.ini`. Para no realizar el seguimiento de todas las aplicaciones (por ejemplo, para evitar la divulgación de información confidencial de los usuarios), puede llevar a cabo este proceso en una instancia de aplicación individual indicando la ubicación de un archivo `odbcinst.ini` privado mediante la variable de entorno `ODBCSYSINI`. Por ejemplo:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

En este caso, puede agregar `Trace=Yes` a la `[ODBC Driver 13 for SQL Server]` sección de `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinación del archivo ODBC.ini que está utilizando el controlador

Los controladores ODBC de Linux y MacOS no saben cuál `odbc.ini` está en uso o la ruta de acceso `odbc.ini` al archivo. Sin embargo, la información `odbc.ini` sobre qué archivo está en uso está disponible en las `odbc_config` herramientas `odbcinst`de unixODBC y, y en la documentación del administrador de controladores de unixODBC.

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

En la [documentación de unixODBC](http://www.unixodbc.org/doc/UserManual/) se explican las diferencias entre los DSN de usuario y del sistema. En Resumen:

- Los DSN de usuario---estos son DSN que solo están disponibles para un usuario específico. Los usuarios pueden conectarse mediante, agregar, modificar y quitar sus propios DSN de usuario. Los DSN de usuario se almacenan en un archivo en el directorio principal del usuario o en un subdirectorio.

- Los DSN del sistema---estos DSN están disponibles para que todos los usuarios del sistema se conecten con ellos, pero un administrador del sistema solo puede agregarlos, modificarlos y quitarlos. Si un usuario tiene un DSN de usuario con el mismo nombre que un DSN de sistema, el DSN de usuario se usará en las conexiones del usuario.

## <a name="see-also"></a>Consulte también

- [Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
