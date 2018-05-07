---
title: Obtener la versión del controlador | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 786b1db3787ff2945cae29980b8ab593032737f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getting-the-driver-version"></a>Obtener la versión del controlador
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  La versión de la instalación [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] puede encontrarse en las siguientes maneras:  
  
-   Llame a la [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) métodos [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md), o [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   La versión se muestra en el archivo readme.txt de la distribución del producto.  
  
 Además, se puede devolver el nombre del controlador JDBC desde la [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) llamada al método en la clase SQLServerDatabaseMetaData. Devolverá, por ejemplo, "Microsoft JDBC Driver 6.4 para SQL Server".  
  
 El siguiente es un ejemplo de la salida de las llamadas a los métodos de la clase SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Donde "xxx.x" es el número de la versión final.  
  
## <a name="see-also"></a>Vea también  
 [Diagnosticar problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
