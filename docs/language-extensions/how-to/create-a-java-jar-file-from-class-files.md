---
title: Creación de un archivo .jar de Java a partir de archivos de clase
titleSuffix: SQL Server Language Extensions
description: Cómo crear un archivo .jar de Java a partir de archivos de clase
author: dphansen
ms.author: davidph
ms.date: 07/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cec311a28f9d5119b5a0aeb696597e8b34ba25a
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "73588779"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Creación de un archivo .jar de Java a partir de archivos de clase
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Al usar [extensiones de lenguaje de SQL Server](../language-extensions-overview.md) y ejecutar código Java, se recomienda empaquetar los archivos de clase en un archivo .jar.

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

+ [Cómo llamar a Java en SQL Server](../how-to/call-java-from-sql.md)