---
title: Creación de un archivo .jar de Java a partir de archivos de clase
description: Cómo crear un archivo .jar de Java a partir de archivos de clase
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53eb4b8da04a799461dcb1e0cb32feff2fe6f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "73658868"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Creación de un archivo .jar de Java a partir de archivos de clase
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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