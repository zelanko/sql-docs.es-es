---
title: Creación de un archivo .jar de Java a partir de archivos de clase
description: Empaquete los archivos de clase en un archivo .jar al usar extensiones de lenguaje de SQL Server para ejecutar código de Java.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c324fca6893af35cafe6e9f65eccd0e8a0e478f9
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180288"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Creación de un archivo .jar de Java a partir de archivos de clase
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Obtenga información sobre cómo empaquetar los archivos de clase en un archivo jar, al usar las [extensiones de lenguaje de SQL Server](../language-extensions-overview.md) para ejecutar código Java. Se recomienda empaquetar los archivos.

## <a name="create-a-jar-file"></a>Creación de un archivo .jar de Java

Para crear un archivo .jar a partir de archivos de clase, vaya a la carpeta que contenga el archivo de clase y ejecute el comando siguiente:

```cmd
jar -cf <MyJar.jar> *.class
```

Asegúrese de que la ruta de acceso a `jar.exe` forme parte de la variable de la ruta de acceso del sistema. También puede especificar la ruta de acceso completa a .jar, que se encuentra en `/bin`, en la carpeta JDK. Por ejemplo:

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>Pasos siguientes

+ [Procedimiento para llamar al tiempo de ejecución de Java en las extensiones de lenguaje de SQL Server](../how-to/call-java-from-sql.md)