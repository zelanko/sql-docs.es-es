---
title: Usar T-SQL (crear biblioteca externa) para instalar paquetes de R
description: Agregue nuevos paquetes de R a SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (in-Database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/12/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 80af3f93eb84c7b78c5cb1e5395175501931e24c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470088"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>Usar T-SQL (crear biblioteca externa) para instalar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se explica cómo instalar nuevos paquetes de R en una instancia de SQL Server en la que el aprendizaje automático está habilitado. Hay varios enfoques entre los que elegir. El uso de T-SQL funciona mejor para los administradores de servidores que no están familiarizados con R.

**Se aplica a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]  [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

La instrucción [Create external library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) permite agregar un paquete o un conjunto de paquetes a una instancia de o a una base de datos específica sin ejecutar código de R o Python directamente. Sin embargo, este método requiere la preparación del paquete y permisos de base de datos adicionales.

+ Todos los paquetes deben estar disponibles como archivos comprimidos locales, en lugar de descargarse a petición desde Internet.

+ Todas las dependencias deben identificarse por el nombre y la versión, y se pueden incluir en el archivo zip. Se produce un error en la instrucción si los paquetes necesarios no están disponibles, incluidas las dependencias de paquetes de nivel inferior. 

+ Debe ser **db_owner** o tener el permiso CREATE external library en un rol de base de datos. Para obtener más información, consulte [Create external library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Descargar paquetes en formato de archivo

Si va a instalar un único paquete, descargue el paquete en formato comprimido.

Es más común instalar varios paquetes debido a las dependencias de paquete. Cuando un paquete requiere otros paquetes, debe comprobar que todos ellos son accesibles entre sí durante la instalación. Se recomienda [crear un repositorio local](create-a-local-package-repository-using-minicran.md) mediante [miniCRAN](https://andrie.github.io/miniCRAN/) para ensamblar una colección completa de paquetes, así como [igraph](https://igraph.org/r/) para analizar las dependencias de los paquetes. La instalación de una versión incorrecta de un paquete o la omisión de una dependencia del paquete puede producir un error en una instrucción CREATE EXTERNAL LIBRARY. 

## <a name="copy-the-file-to-a-local-folder"></a>Copiar el archivo en una carpeta local

Copie el archivo comprimido que contiene todos los paquetes en una carpeta local del servidor. Si no tiene acceso al sistema de archivos en el servidor, también puede pasar un paquete completo como una variable, con un formato binario. Para obtener más información, consulte [Create external library](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Ejecutar la instrucción para cargar paquetes

Abra una ventana de **consulta** mediante una cuenta con privilegios administrativos.

Ejecute la instrucción `CREATE EXTERNAL LIBRARY` T-SQL para cargar la colección de paquetes comprimidos en la base de datos.

Por ejemplo, los siguientes nombres de instrucción como el origen del paquete son un repositorio de miniCRAN que contiene el paquete **randomForest** , junto con sus dependencias. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

No se puede usar un nombre arbitrario; el nombre de la biblioteca externa debe tener el mismo nombre que se espera usar al cargar o llamar al paquete.

## <a name="verify-package-installation"></a>Comprobar la instalación del paquete

Si la biblioteca se ha creado correctamente, puede ejecutar el paquete en SQL Server, llamándolo dentro de un procedimiento almacenado.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Vea también

+ [Obtención de información del paquete](../package-management/installed-package-information.md)
+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
