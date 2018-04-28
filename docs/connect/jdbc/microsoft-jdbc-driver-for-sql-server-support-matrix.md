---
title: Microsoft JDBC Driver para SQL Server Support Matrix | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 84c06f5153d47c82a268a0b5e20e74b4e32d6685
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Matriz de compatibilidad de Microsoft JDBC Driver para SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta página contiene la matriz de compatibilidad y la directiva de ciclo de vida de soporte de Microsoft JDBC Driver para SQL Server.  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Directiva y matriz de ciclo de vida de soporte de Microsoft JDBC Driver  
 La directiva de ciclo de vida de soporte de Microsoft (MSL) proporciona información transparente y predecible sobre el ciclo de vida de soporte de productos de Microsoft. Versiones del controlador JDBC 3.0, 4.x y 6.x tienen cinco años de soporte estándar del controlador de la fecha de lanzamiento. El soporte estándar se define en el sitio web del ciclo de vida de soporte de Microsoft.  
  
 Las opciones de soporte extendido y personalizado no están disponibles para Microsoft JDBC Driver.  
    
 Se admiten los siguientes controladores Microsoft JDBC Driver hasta la fecha de finalización del soporte.  
  
|Nombre del controlador|Versión del paquete de controladores|JAR(s) aplicable|Finalización del soporte estándar|
|-|-|-|-|  
|Microsoft JDBC Driver 6.4 para SQL Server|6.4|MSSQL-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|22 de enero de 2023|    
|Microsoft JDBC Driver 6.2 para SQL Server|6.2|MSSQL-jdbc-6.2.2.jre8.jar<br> MSSQL-jdbc-6.2.2.jre7.jar|30 de junio de 2022|    
|Microsoft JDBC Driver 6.0 para SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|14 de julio de 2021|    
|Microsoft JDBC Driver 4.2 para SQL Server|4.2|sqljdbc42.jar<br>sqljdbc41.jar|24 de agosto de 2020|  
|Controlador JDBC 4.1 de Microsoft para SQL Server|4.1|sqljdbc41.jar|12 de diciembre de 2019|  
  
 Ya no se admiten los siguientes controladores Microsoft JDBC Driver.  
 
|Nombre del controlador|Versión del paquete de controladores|Finalización del soporte estándar|  
|-|-|-|
|Microsoft JDBC Driver 4.0 para SQL Server|4.0|6 de marzo de 2017|  
|Controlador JDBC de Microsoft SQL Server 3.0|3.0|23 de abril de 2015|  
|Microsoft JDBC Driver 2.0 para SQL Server|2.0|31 de diciembre de 2012|  
|Controlador JDBC de Microsoft SQL Server 2005 versión 1.2|1.2|25 de junio de 2011|  
|Microsoft JDBC Driver 1.1 para SQL Server 2005|1.1|25 de junio de 2011|  
|Microsoft JDBC Driver 1.0 para SQL Server 2005|1,0|25 de junio de 2011|  
|Microsoft JDBC Driver para SQL Server 2000|2000|9 de julio de 2010|  
  
## <a name="sql-version-compatibility"></a>Compatibilidad con versiones de SQL  
  
|Versión del controlador|SQL Server 2008|SQL Server 2008 R2|SQL Server 2012|Azure SQL Database|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|SQL Azure administra la instancia (vista previa privada de extendida)|  
|-|-|-|-|-|-|-|-|-|-|
|6.4|N|S|S|S|S|S|S|S|S|  
|6.2|S|S|S|S|S|S|S|S|N|
|6.1|S|S|S|S|S|S|S|N|N|
|6.0|S|S|S|S|S|S|S|N|N|
|4.2|S|S|S|S|S|S|S|N|N|
|4.1|S|S|S|S|S|S|S|N|N|
|4.0|S|S|S|S|S|S|S|N|N|
|3.0|S|S|Y<sup>1</sup>|Y<sup>2</sup>|N|Y<sup>5</sup>|N|N|N|
|2.0|Y<sup>3</sup>|Y<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|Y<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|  
|1,0|N|N|N|N|N|N|N|N|N|  
|2000|N|N|N|N|N|N|N|N|N|  
  
 <sup>1</sup>versión 3.0 de controlador de JDBC de Microsoft SQL Server puede conectarse a SQL Server 2012 como un cliente de nivel inferior.  
  
 <sup>2</sup>compatibilidad de base de datos de SQL Azure se introdujo en la versión 3.0 del controlador como una revisión. Se recomienda que los clientes de Base de datos SQL de Azure usen la versión más reciente del controlador que haya disponible.  
  
 <sup>3</sup>controlador JDBC de Microsoft SQL Server versión 2.0 y Microsoft SQL Server 2005 JDBC Driver versión 1.2 pueden conectarse a SQL Server 2008 como un cliente de nivel inferior. Cuando se permiten las conversiones de nivel inferior, las aplicaciones pueden ejecutar consultas y realizar actualizaciones en los nuevos tipos de datos de SQL Server 2008, como time, date, datetime2, datetimeoffset y FILESTREAM. Para obtener más información sobre cómo utilizar estos nuevos tipos de datos con el controlador JDBC, consulte  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver](http://go.microsoft.com/fwlink/?LinkId=145198) (Operaciones con los tipos de datos de fecha y hora de SQL Server 2008 utilizando Microsoft JDBC Driver) y  [Working with SQL Server 2008 FileStream using JDBC Driver](http://go.microsoft.com/fwlink/?LinkId=145199)(Operaciones con datos FILESTREAM de SQL Server 2008 utilizando Microsoft JDBC Driver). Para obtener más información sobre la compatibilidad de nivel inferior de estos nuevos tipos de datos, consulte los temas de los Libros en pantalla de SQL Server  [Usar datos de fecha y hora](http://go.microsoft.com/fwlink/?LinkId=145211)y  [Compatibilidad con FILESTREAM](http://go.microsoft.com/fwlink/?LinkId=145212) .  
  
 <sup>4</sup>compatibilidad para las conexiones entre el controlador JDBC de Microsoft y el almacenamiento de datos paralelos se introdujo en Microsoft JDBC Driver 4.0 para SQL Server y Microsoft SQL Server 2008 R2 paralelo datos almacenamiento dispositivo Update 3.  
  
 <sup>5</sup>versión 3.0 de controlador de JDBC de Microsoft SQL Server puede conectarse a SQL Server 2014 como un cliente de nivel inferior.  
  
## <a name="java-and-jdbc-specification-support"></a>Compatibilidad con especificaciones de JDBC y Java  
  
|Versión de Microsoft JDBC Driver|Versiones de JRE|Versión de la API de JDBC| 
|-|-|-|  
|6.4|1.7, 1.8, 1.9|4.1, 4.2, 4.3 (parcial)|  
|6.2|1.7, 1.8|4.1, 4.2|  
|6.1|1.7, 1.8|4.1, 4.2|  
|6.0|1.7, 1.8|4.1, 4.2|  
|4.2|1.7, 1.8|4.1, 4.2|  
|4.1|1.7|4.0|  
|4.0|1.5, 1.6, 1.7|3.0, 4.0|  
|3.0|1.5, 1.6,|3.0, 4.0|  
|2.0|1.5, 1.6|3.0, 4.0|  
|1.2|1.4, 1.5, 1.6|3.0|  
|1.1|1.4|3.0|  
|1,0|1.4|3.0|  
|2000|1.4|3.0|  
  
## <a name="supported-operating-systems"></a>Sistemas operativos admitidos  
 Microsoft JDBC Driver se ha diseñado para que funcione en cualquier sistema operativo que admita el uso de una máquina virtual Java (JVM). Algunas de las plataformas que más se utilizan son, por ejemplo, Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2008 R2, Windows Vista, Linux, Unix, AIX y MacOS.  
  
 El equipo del producto JDBC comprueba nuestro controlador en Windows, Sun Solaris, SUSE Linux y RedHat Linux.  El servicio de asistencia al cliente está disponible para clientes de todas las plataformas; sin embargo, es posible que le pidamos que reproduzca el problema en una plataforma concreta, como Windows.  
  
## <a name="application-server-support"></a>Compatibilidad con servidores de aplicaciones  
 Microsoft JDBC Driver for SQL Server se ha probado con varios servidores de aplicaciones.  Pídale a su proveedor de servidores de aplicaciones más información sobre qué versión del controlador es compatible con su producto.  
  
  
