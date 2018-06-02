---
title: Usar T-SQL (crear biblioteca externa) para instalar paquetes de R en los servicios de aprendizaje de máquina de SQL Server | Documentos de Microsoft
description: Agregar nuevos paquetes de R para SQL Server de 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7a5a0c394e9a26244661a4ae712d20583c1f1c99
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585487"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>Usar T-SQL (crear biblioteca externa) para instalar paquetes de R en servicios de aprendizaje de máquina de SQL Server de 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo instalar nuevos paquetes de R en una instancia de SQL Server donde está habilitado el aprendizaje automático. Existen varios enfoques que puede elegir. Mediante T-SQL funciona mejor para los administradores del servidor que no estén familiarizados con R.

**Se aplica a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

El [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción hace posible agregar un paquete o un conjunto de paquetes a una instancia o una base de datos sin ejecutar código R o directamente el código Python. Sin embargo, este método requiere la preparación del paquete y los permisos de base de datos adicional.

+ Todos los paquetes deben estar disponibles como un archivo comprimido local, en lugar de descargado a petición desde internet.

+ Todas las dependencias deben ser identificadas por el nombre y la versión e incluidas en el archivo zip. La instrucción produce un error si los paquetes necesarios no están disponibles, incluidas las dependencias de paquete de nivel inferior. 

+ Debe ser **db_owner** o tener el permiso de crear una biblioteca externa en un rol de base de datos. Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Descargar los paquetes en formato de archivo

Si va a instalar un único paquete, descargue el paquete en formato comprimido.

Es más habitual para instalar varios paquetes debido a las dependencias del paquete. Cuando un paquete requiere otros paquetes, debe comprobar que todas ellas son accesibles entre sí durante la instalación. Se recomienda [creando un repositorio local](create-a-local-package-repository-using-minicran.md) con [miniCRAN](http://andrie.github.io/miniCRAN/) para ensamblar una recolección completa de paquetes, así como [igraph](http://igraph.org/r/) para analizar las dependencias de paquetes. Instalar una versión incorrecta de un paquete o si se omite una dependencia del paquete puede producir un error en una instrucción crear biblioteca externa. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie el archivo en una carpeta local

Copie el archivo comprimido que contiene todos los paquetes en una carpeta local en el servidor. Si no tiene acceso al sistema de archivos en el servidor, también puede pasar un paquete completo como una variable, usando un formato binario. Para obtener más información, consulte [crear biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Ejecute la instrucción para cargar paquetes

Abra un **consulta** ventana, con una cuenta con privilegios administrativos.

Ejecute la instrucción de T-SQL `CREATE EXTERNAL LIBRARY` para cargar la recopilación del paquete comprimido en la base de datos.

Por ejemplo, la siguiente instrucción nombres como el origen del paquete un repositorio de miniCRAN que contiene el **randomForest** paquete, junto con sus dependencias. 

```SQL
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

No se puede usar un nombre arbitrario; el nombre de biblioteca externa debe tener el mismo nombre que se espera que se utilizará al cargar o el paquete de la llamada.

## <a name="verify-package-installation"></a>Comprobar la instalación del paquete

Si la biblioteca se haya creado correctamente, puede ejecutar el paquete en SQL Server, si lo llaman dentro de un procedimiento almacenado.
    
```SQL
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Vea también

+ [Obtención de información del paquete](determine-which-packages-are-installed-on-sql-server.md)
+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Guías de procedimientos](sql-server-machine-learning-tasks.md)