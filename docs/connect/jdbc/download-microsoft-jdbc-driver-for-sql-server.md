---
title: Descarga de Microsoft JDBC Driver para SQL Server
description: Descargue Microsoft JDBC Driver para SQL Server para desarrollar aplicaciones Java que se conecten a SQL Server.
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcf034b332494750885d4808b54c9cb62c37077c
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/04/2020
ms.locfileid: "77013120"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Descarga de Microsoft JDBC Driver para SQL Server

En este artículo se proporcionan vínculos de descarga a Microsoft JDBC Driver para SQL Server. Este controlador le permite desarrollar aplicaciones Java que se conecten a SQL Server.  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>Descargas disponibles del controlador JDBC Driver para SQL Server

Use los vínculos de la siguiente tabla para descargar la versión más reciente de Microsoft JDBC Driver para SQL Server que coincida con su entorno Java Runtime Environment (JRE):

| Versión | Fecha de la versión | Versiones de Java |
|---|---|---|
| [Microsoft JDBC Driver 8.2](https://go.microsoft.com/fwlink/?linkid=2116870) | 31/1/2020 | JRE 8, 11, 13 |
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 1/8/2019 | JRE 8, 11, 12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 17/4/2019 | JRE 8, 11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 31/7/2018 | JRE 8, 10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 26/3/2018 | JRE 7, 8, 9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 12/2/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 27/2/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 4.2](https://go.microsoft.com/fwlink/?linkid=841534) | 26/2/2018 | JRE 7, 8 |

Al descargar el controlador, hay varios archivos JAR. El nombre del archivo JAR indica la versión de Java que admite. Para obtener más información sobre cada versión, consulte las [notas de la versión](release-notes-for-the-jdbc-driver.md) y los [requisitos del sistema](system-requirements-for-the-jdbc-driver.md).

## <a name="using-the-jdbc-driver-with-maven-central"></a>Uso del controlador JDBC con Maven Central

El controlador JDBC se puede agregar a un proyecto de Maven si se incorpora como una dependencia en el archivo POM.xml con el siguiente código:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.2.0.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>Controladores no compatibles

Las versiones de controladores no compatibles no están disponibles para descargarse aquí. Estamos trabajando continuamente para mejorar la compatibilidad con la conectividad de Java. Por tanto, se recomienda encarecidamente trabajar con la versión más reciente de Microsoft JDBC Driver.  
  
## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Microsoft JDBC Driver para SQL Server, consulte [Introducción al controlador JDBC](overview-of-the-jdbc-driver.md) y el [repositorio de GitHub del controlador JDBC](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md).
