---
title: Seguimiento de acceso a datos con el controlador ODBC en Linux y macOS
description: Obtenga información sobre cómo habilitar el seguimiento en Linux y macOS con Microsoft ODBC Driver for SQL Server para generar un archivo de registro al solucionar problemas relativos al comportamiento de la aplicación.
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69f55104ed73f4d6468de3dcacca54d05cf0ac9a
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288212"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Seguimiento de acceso a datos con el controlador ODBC en Linux y macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

El Administrador de controladores unixODBC en macOS y Linux admite el seguimiento de la entrada de llamadas de la API de ODBC y la salida del controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Para realizar un seguimiento del comportamiento de ODBC de la aplicación, edite la sección `[ODBC]` del archivo `odbcinst.ini` para establecer los valores `Trace=Yes` y `TraceFile` en la ruta de acceso del archivo que va a contener la salida de seguimiento; por ejemplo:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(También puede usar `/dev/stdout` o cualquier otro nombre de dispositivo para enviar la salida de seguimiento allí, en lugar de a un archivo persistente). Con la configuración anterior, cada vez que una aplicación carga el Administrador de controladores unixODBC, registra todas las llamadas API de ODBC que se hayan realizado en el archivo de salida.

Cuando termine de realizar el seguimiento de la aplicación, quite `Trace=Yes` del archivo `odbcinst.ini` para evitar penalizaciones en el rendimiento de seguimiento, y asegúrese de que se quitan los archivos de seguimiento innecesarios.

El seguimiento se aplica a todas las aplicaciones que utilizan el controlador de `odbcinst.ini`. Para no realizar el seguimiento de todas las aplicaciones (por ejemplo, para evitar la divulgación de información confidencial de los usuarios), puede llevar a cabo este proceso en una instancia de aplicación individual indicando la ubicación de un archivo `odbcinst.ini` privado mediante la variable de entorno `ODBCSYSINI`. Por ejemplo:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

En este caso, puede agregar `Trace=Yes` a la sección `[ODBC Driver 17 for SQL Server]` de `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinación del archivo ODBC.ini que está utilizando el controlador

Los controladores ODBC de Linux y macOS no saben qué `odbc.ini` está en uso o la ruta de acceso al archivo `odbc.ini`. Sin embargo, la información sobre qué archivo `odbc.ini` está en uso está disponible en las herramientas de unixODBC `odbc_config` y `odbcinst`, y en la documentación del Administrador de controladores unixODBC.

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

La [documentación de unixODBC](http://www.unixodbc.org/doc/UserManual/) explica las diferencias entre los DSN del usuario y del sistema. En resumen:

- Los DSN de usuario son DSN que solo están disponibles para un usuario específico. Los usuarios pueden conectarse con sus propios DND de usuario, así como agregarlos, modificarlos y quitarlos. Los DSN de usuario se almacenan en un archivo en el directorio principal del usuario o en un subdirectorio de este.

- Los DSN del sistema son DSN que están disponibles para que todos los usuarios del sistema se conecten con ellos, pero solo un administrador del sistema puede agregarlos, modificarlos y quitarlos. Si un usuario tiene un DSN de usuario con el mismo nombre que un DSN del sistema, el DSN de usuario se usará en las conexiones de ese usuario.

## <a name="see-also"></a>Consulte también

- [Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
