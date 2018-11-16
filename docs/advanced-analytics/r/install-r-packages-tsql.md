---
title: Utilizar T-SQL (crear biblioteca externa) para instalar paquetes de R en SQL Server Machine Learning Services | Documentos de Microsoft
description: Agregar nuevos paquetes de R a 2017 máquina Learning Services (en bases de datos) de SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 897bafaaf5ec32c417bb5d9625ce6cef22d6e783
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699393"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>Utilizar T-SQL (crear biblioteca externa) para instalar paquetes de R en 2017 máquina Learning Services de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo instalar nuevos paquetes de R en una instancia de SQL Server donde está habilitado el aprendizaje automático. Hay varios enfoques que puede elegir. Utilizar T-SQL funciona mejor para los administradores de servidores que no están familiarizados con R.

**Se aplica a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

La [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción hace posible agregar un paquete o un conjunto de paquetes a una instancia o una base de datos sin ejecutar R o directamente el código Python. Sin embargo, este método requiere preparación del paquete y los permisos de base de datos adicional.

+ Todos los paquetes deben ser disponible como un archivo zip local, en lugar de descargados a petición desde internet.

+ Todas las dependencias deben ser identificadas por nombre y versión e incluidas en el archivo zip. La instrucción produce un error si es necesario que los paquetes no están disponibles, incluidas las dependencias de paquete de nivel inferior. 

+ Debe ser **db_owner** o tener el permiso de crear biblioteca externa en una función de base de datos. Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Descargue los paquetes en formato de archivo

Si va a instalar un único paquete, descargue el paquete en formato zip.

Es más común que instalar varios paquetes debido a las dependencias de paquetes. Cuando un paquete requiere otros paquetes, debe comprobar que todos ellos son accesibles entre sí durante la instalación. Se recomienda [crear un repositorio local](create-a-local-package-repository-using-minicran.md) con [miniCRAN](https://andrie.github.io/miniCRAN/) a reunir una colección completa de los paquetes, así como [igraph](https://igraph.org/r/) para el análisis de las dependencias de paquetes. Instalar la versión incorrecta de un paquete o si se omite una dependencia del paquete puede causar una instrucción crear biblioteca externa de un error. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie el archivo en una carpeta local

Copie el archivo comprimido que contiene todos los paquetes en una carpeta local en el servidor. Si no tiene acceso al sistema de archivos en el servidor, se puede pasar un paquete completo como una variable, usando un formato binario. Para obtener más información, consulte [crear biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Ejecute la instrucción para cargar paquetes

Abrir una **consulta** ventana, utilizando una cuenta con privilegios administrativos.

Ejecute la instrucción SQL de T `CREATE EXTERNAL LIBRARY` para cargar la recopilación del paquete comprimido en la base de datos.

Por ejemplo, la siguiente instrucción asigna como origen del paquete un repositorio de miniCRAN que contiene el **randomForest** paquete, junto con sus dependencias. 

```SQL
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

No se puede utilizar un nombre arbitrario; el nombre de biblioteca externa debe tener el mismo nombre que espera utilizar al cargar o llamando el paquete.

## <a name="verify-package-installation"></a>Compruebe la instalación del paquete

Si la biblioteca se crea correctamente, puede ejecutar el paquete en SQL Server, llamando dentro de un procedimiento almacenado.
    
```SQL
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Vea también

+ [Obtención de información del paquete](determine-which-packages-are-installed-on-sql-server.md)
+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Guías de procedimientos](sql-server-machine-learning-tasks.md)