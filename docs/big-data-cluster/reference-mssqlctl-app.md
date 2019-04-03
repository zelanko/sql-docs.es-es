---
title: referencia de aplicación mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de la aplicación de mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b418f1ded8d9911143b431ae9793c467c4e26eb4
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860656"
---
# <a name="mssqlctl-app"></a>Aplicación mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **aplicación** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [crear](#create) | Crear la aplicación. |
| [eliminar](#delete) | Eliminar la aplicación. |
| [describe](#describe) | Describir la aplicación. |
| [Init](#init) | Nueva aplicación KickStart esqueleto. |
| [enumerar](#list) | Lista de aplicaciones. |
| [ejecutar](#run) | Ejecutar la aplicación. |
| [update](#update) | Actualizar la aplicación. |
| [plantilla](reference-mssqlctl-app-template.md) | Comandos de la plantilla. |

## <a id="create"></a> Crear aplicación mssqlctl

Crear la aplicación.

```
mssqlctl app create
   --assets
   --code
   --description
   --entrypoint
   --inputs
   --name
   --outputs
   --runtime
   --spec
   --version
   --yes
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--activos - a** | Lista de recursos del archivo de aplicación adicional que se incluya. |
| **--code -c** | Ruta de acceso al archivo de código R o Python. |
| **--description -d** | Descripción de la aplicación. |
| **--entrypoint** |  |
| **--entradas** | Esquema de parámetros de entrada. |
| **: nombre - n** | Nombre de aplicación. |
| **--salidas** | Esquema de parámetros de salida. |
| **--en tiempo de ejecución - r** | Tiempo de ejecución de la aplicación.  Valores permitidos: Mleap, Python, R, SSIS. |
| **--spec -s** | Ruta de acceso a un directorio con un archivo de YAML especificación que describe la aplicación. |
| **--versión - v** | Versión de la aplicación. |
| **--Sí -y** | No solicita confirmación al crear una aplicación del archivo de spec.yaml del CWD. |

### <a name="examples"></a>Ejemplos

Cree una nueva aplicación a través de spec.yaml (recomendado).

```
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```

Crear un nuevo insertadas de aplicación de Python con argumentos.

```
mssqlctl app create --name add --version v1 --inputs x=float, y=float --outputs result=float --runtime Python --code add.py  --init init.py
```

Crear un nuevo insertadas de aplicación de R con argumentos.

```
mssqlctl app create --name add --version v1 --inputs x=numeric, y=numeric --outputs result=numeric --runtime R --code add.R  --init init.R
```

Crear un nuevo insertadas de aplicación de R con recursos de archivo adicionales que se incluya.

```
mssqlctl app create --name add --version v1 --runtime R --code  add.R --assets file.RData,/path/to/more/files
```

## <a id="delete"></a> mssqlctl app delete

Eliminar la aplicación.

```
mssqlctl app delete
   --name
   --version
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **: nombre - n** | Nombre de aplicación. |
| **--versión - v** | Versión de la aplicación. |

### <a name="examples"></a>Ejemplos

Eliminar la aplicación por nombre y versión.

```
mssqlctl app delete --name reduce --version v1
```

## <a id="describe"></a> Describir la aplicación mssqlctl

Describir la aplicación.

```
mssqlctl app describe
   --name
   --spec
   --version
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **: nombre - n** | Nombre de aplicación. |
| **--spec -s** | Ruta de acceso a un directorio con un archivo de YAML especificación que describe la aplicación. |
| **--versión - v** | Versión de la aplicación. |

### <a name="examples"></a>Ejemplos

Descripción de la aplicación.

```
mssqlctl app describe --name reduce --version v1
```

## <a id="init"></a> mssqlctl aplicación init

Nueva aplicación KickStart esqueleto.

```
mssqlctl app init
   --destination
   --name
   --spec
   --template
   --url
   --version
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--destino -d** | Dónde colocar el esqueleto de la aplicación. Valor predeterminado: directorio de trabajo actual. |
| **: nombre - n** | Nombre de aplicación. |
| **--spec -s** | Generar simplemente una spec.yaml de aplicación. |
| **--template -t** | Nombre de la plantilla. Para obtener una lista completa desactivar los nombres de plantilla admitidos, ejecute `mssqlctl app template list`. |
| **--url -u** | Especifique una ubicación de repositorio de plantillas diferentes. Valor predeterminado: https://github.com/Microsoft/sql-server-samples.git. |
| **--versión - v** | Versión de la aplicación. |

### <a name="examples"></a>Ejemplos

Aplicar scaffolding a una nueva aplicación `spec.yaml` solo.

```
mssqlctl app init --spec
```

Aplicar la técnica scaffolding en función de un esqueleto de aplicación de aplicación de nuevo R el `r` plantilla.

```
mssqlctl app init --name reduce --template r
```

Aplicar la técnica scaffolding un esqueleto de aplicación de aplicación de Python nuevo según la `python` plantilla.

```
mssqlctl app init --name reduce --template python
```

Aplicar la técnica scaffolding SSIS aplicación aplicación esqueleto nuevo según la `ssis` plantilla.

```
mssqlctl app init --name reduce --template ssis
```

## <a id="list"></a> lista de aplicaciones mssqlctl

Lista de aplicaciones.

```
mssqlctl app list
   --name
   --version
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **: nombre - n** | Nombre de aplicación. |
| **--versión - v** | Versión de la aplicación. |

### <a name="examples"></a>Ejemplos

Aplicación de lista por nombre y versión.

```
mssqlctl app list --name reduce  --version v1
```

Enumerar todas las versiones de la aplicación por su nombre.

```
mssqlctl app list --name reduce
```

Enumera todas las aplicaciones.

```
mssqlctl app list
```

## <a id="run"></a> ejecución de la aplicación mssqlctl

Ejecutar la aplicación.

```
mssqlctl app run
   --name
   --version
   --inputs
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **: nombre - n** | Nombre de aplicación. |
| **--versión - v** | Versión de la aplicación. |
| **--entradas** | Aplicación de parámetros de entrada en un archivo CSV `name=value` formato. |

### <a name="examples"></a>Ejemplos

Ejecute la aplicación con ningún parámetro de entrada.

```
mssqlctl app run --name reduce --version v1
```

Ejecute la aplicación con 1 parámetro de entrada.

```
mssqlctl app run --name reduce --version v1 --inputs x=10
```

Ejecutar la aplicación con varios parámetros de entrada.

```
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6
```

## <a id="update"></a> mssqlctl app update

Actualizar la aplicación.

```
mssqlctl app update
   --spec
   --yes
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--spec -s** | Ruta de acceso a un directorio con un archivo de YAML especificación que describe la aplicación. |
| **--Sí -y** | No solicita confirmación al actualizar una aplicación partir spec.yaml archivo del CWD. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).