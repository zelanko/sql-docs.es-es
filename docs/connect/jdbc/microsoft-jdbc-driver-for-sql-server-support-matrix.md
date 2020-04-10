---
title: Matriz de compatibilidad de Microsoft JDBC Driver para SQL Server
ms.custom: ''
ms.date: 03/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f9482c80d3ea84b814857433f6ff2a0389cc544
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922839"
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Matriz de compatibilidad de Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta página contiene la matriz de compatibilidad y la directiva de ciclo de vida de soporte de Microsoft JDBC Driver para SQL Server.  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Directiva y matriz de ciclo de vida de soporte de Microsoft JDBC Driver  

La directiva de ciclo de vida de soporte de Microsoft (MSL) proporciona información transparente y predecible sobre el ciclo de vida de soporte de productos de Microsoft. Las versiones 3.0, 4.x, 6.x, 7.x y 8.x del controlador JDBC incluyen cinco años de soporte técnico estándar a partir de la fecha de publicación del controlador. El soporte técnico estándar se define en el sitio web del ciclo de vida de soporte técnico de Microsoft.  
  
Las opciones de soporte extendido y personalizado no están disponibles para Microsoft JDBC Driver.  

Se admiten los siguientes controladores Microsoft JDBC Driver hasta la fecha de finalización del soporte.  
  
|Nombre del controlador|Versión del paquete de controladores|Archivos JAR aplicables|Finalización del soporte estándar|
|-|-|-|-|  
|Microsoft JDBC Driver 8.2 para SQL Server|8,2|mssql-jdbc-8.2.2.jre13.jar<br> mssql-jdbc-8.2.2.jre11.jar<br> mssql-jdbc-8.2.2.jre8.jar|24 de marzo de 2025|
|Microsoft JDBC Driver 7.4 para SQL Server|7.4|mssql-jdbc-7.4.1.jre12.jar<br> mssql-jdbc-7.4.1.jre11.jar<br> mssql-jdbc-7.4.1.jre8.jar|2 de agosto de 2024|
|Microsoft JDBC Driver 7.2 para SQL Server|7.2|mssql-jdbc-7.2.2.jre11.jar<br> mssql-jdbc-7.2.2.jre8.jar|16 de abril de 2024|
|Microsoft JDBC Driver 7.0 para SQL Server|7.0|mssql-jdbc-7.0.0.jre10.jar<br> mssql-jdbc-7.0.0.jre8.jar|31 de julio de 2023|
|Microsoft JDBC Driver 6.4 para SQL Server|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|27 de febrero de 2023|
|Microsoft JDBC Driver 6.2 para SQL Server|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|30 de junio de 2022|
|Microsoft JDBC Driver 6.0 para SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|14 de julio de 2021|
|Microsoft JDBC Driver 4.2 para SQL Server|4,2|sqljdbc42.jar<br>sqljdbc41.jar|24 de agosto de 2020|
  
 Ya no se admiten los siguientes controladores Microsoft JDBC Driver.  

|Nombre del controlador|Versión del paquete de controladores|Finalización del soporte estándar|  
|-|-|-|
|Controlador JDBC 4.1 de Microsoft para SQL Server|4,1|12 de diciembre de 2019|  
|Microsoft JDBC Driver 4.0 para SQL Server|4.0|6 de marzo de 2017|  
|Controlador JDBC de Microsoft SQL Server 3.0|3.0|23 de abril de 2015|  
|Microsoft JDBC Driver 2.0 para SQL Server|2.0|31 de diciembre de 2012|  
|Controlador JDBC de Microsoft SQL Server 2005 versión 1.2|1.2|25 de junio de 2011|  
|Microsoft JDBC Driver 1.1 para SQL Server 2005|1.1|25 de junio de 2011|  
|Microsoft JDBC Driver 1.0 para SQL Server 2005|1.0|25 de junio de 2011|  
|Microsoft JDBC Driver para SQL Server 2000|2000|9 de julio de 2010|  
  
## <a name="sql-version-compatibility"></a>Compatibilidad con versiones de SQL  
  
|Versión del controlador|SQL Server 2008|SQL Server 2008 R2|SQL Server 2012|Azure SQL Database|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|SQL Server 2019|  
|-|-|-|-|-|-|-|-|-|-|-|
|8,2|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.4|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.2|N|Y|Y|Y|Y|Y|Y|Y|N|
|7.0|N|Y|Y|Y|Y|Y|Y|Y|N|
|6.4|N|Y|Y|Y|Y|Y|Y|Y|N|
|6.2|Y|Y|Y|Y|Y|Y|Y|Y|N|
|6.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|6.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|4,2|Y|Y|Y|Y|Y|Y|Y|N|N|
|4,1|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|3.0|Y|Y|S<sup>1</sup>|S<sup>2</sup>|N|S<sup>5</sup>|N|N|N|
|2.0|S<sup>3</sup>|S<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|S<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|
|1.0|N|N|N|N|N|N|N|N|N|
|2000|N|N|N|N|N|N|N|N|N|
  
 <sup>1</sup> Microsoft JDBC Driver 3.0 para SQL Server puede conectarse a SQL Server 2012 como cliente de nivel inferior.  
  
 <sup>2</sup> La compatibilidad con Azure SQL Database se introdujo como revisión en la versión 3.0 del controlador. Se recomienda que los clientes de Base de datos SQL de Azure usen la versión más reciente del controlador que haya disponible.  
  
 <sup>3</sup> Microsoft JDBC Driver 2.0 para SQL Server y Microsoft JDBC Driver 1.2 para SQL Server 2005 pueden conectarse a SQL Server 2008 como cliente de nivel inferior. Cuando se permiten las conversiones de nivel inferior, las aplicaciones pueden ejecutar consultas y realizar actualizaciones en los nuevos tipos de datos de SQL Server 2008, como time, date, datetime2, datetimeoffset y FILESTREAM. Para obtener más información sobre cómo utilizar estos nuevos tipos de datos con el controlador JDBC, consulte  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver](https://go.microsoft.com/fwlink/?LinkId=145198) (Operaciones con los tipos de datos de fecha y hora de SQL Server 2008 utilizando Microsoft JDBC Driver) y  [Working with SQL Server 2008 FileStream using JDBC Driver](https://go.microsoft.com/fwlink/?LinkId=145199)(Operaciones con datos FILESTREAM de SQL Server 2008 utilizando Microsoft JDBC Driver). Para obtener más información sobre la compatibilidad de nivel inferior de estos nuevos tipos de datos, consulte los temas de los Libros en pantalla de SQL Server  [Usar datos de fecha y hora](https://go.microsoft.com/fwlink/?LinkId=145211)y  [Compatibilidad con FILESTREAM](https://go.microsoft.com/fwlink/?LinkId=145212) .  
  
 <sup>4</sup> La compatibilidad con las conexiones entre Microsoft JDBC Driver y el almacenamiento de datos paralelos de Microsoft SQL Server se incluyó por primera vez en Microsoft JDBC Driver 4.0 para SQL Server y la actualización 3 de la aplicación de almacenamiento de datos paralelos de Microsoft SQL Server 2008 R2.  
  
 <sup>5</sup> Microsoft JDBC Driver 3.0 para SQL Server puede conectarse a SQL Server 2014 como cliente de nivel inferior.  
  
## <a name="java-and-jdbc-specification-support"></a>Compatibilidad con especificaciones de JDBC y Java
  
|Versión de Microsoft JDBC Driver|Versiones de JRE|Versión de la API de JDBC|
|-|-|-|
|[8.2](release-notes-for-the-jdbc-driver.md#82)|1.8, 11, 13|4.2, 4.3 (parcialmente)|
|[7.4](release-notes-for-the-jdbc-driver.md#74)|1.8, 11, 12|4.2, 4.3 (parcialmente)|
|[7.2](release-notes-for-the-jdbc-driver.md#72)|1.8, 11|4.2, 4.3 (parcialmente)|
|[7.0](release-notes-for-the-jdbc-driver.md#70)|1.8, 10|4.2, 4.3 (parcialmente)|
|[6.4](release-notes-for-the-jdbc-driver.md#64)|1.7, 1.8, 9|4.1, 4.2, 4.3 (parcialmente)|
|[6.2](release-notes-for-the-jdbc-driver.md#62)|1.7, 1.8|4.1, 4.2|
|[6.1](release-notes-for-the-jdbc-driver.md#61)|1.7, 1.8|4.1, 4.2|
|[6.0](release-notes-for-the-jdbc-driver.md#60)|1.7, 1.8|4.1, 4.2|
|[4.2](release-notes-for-the-jdbc-driver.md#42)|1.7, 1.8|4.1, 4.2|
|4,1|1.7|4.0|
|4.0|1.5, 1.6, 1.7|3.0, 4.0|
|3.0|1.5, 1.6,|3.0, 4.0|
|2.0|1.5, 1.6|3.0, 4.0|
|1.2|1.4, 1.5, 1.6|3.0|
|1.1|1.4|3.0|
|1.0|1.4|3.0|
|2000|1.4|3.0|

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

Microsoft JDBC Driver se ha diseñado para que funcione en cualquier sistema operativo que admita el uso de una máquina virtual Java (JVM). Algunas de las plataformas que más se usan son, por ejemplo, Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2008 R2, Windows Vista, Linux, Unix, AIX y macOS.  

El equipo del producto JDBC comprueba nuestro controlador en Windows, Sun Solaris, SUSE Linux, Ubuntu Linux, CentOS Linux y macOS.

## <a name="application-server-support"></a>Compatibilidad con servidores de aplicaciones

Microsoft JDBC Driver for SQL Server se ha probado con varios servidores de aplicaciones.  Pídale a su proveedor de servidores de aplicaciones más información sobre qué versión del controlador es compatible con su producto.
