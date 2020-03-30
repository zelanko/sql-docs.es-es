---
title: Obtención de la versión del controlador | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db44a391c16a63d28057c99755018179d6c2c0b5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028042"
---
# <a name="getting-the-driver-version"></a>Obtención de la versión del controlador
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  La versión del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] instalado se puede encontrar de las maneras siguientes:  
  
-   Llame a los métodos [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) o [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   La versión se muestra en el archivo readme.txt de la distribución del producto.  
  
 Además, el nombre del controlador JDBC se puede devolver desde la llamada al método [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) de la clase SQLServerDatabaseMetaData. Devolverá, por ejemplo, "Controlador Microsoft JDBC 6.4 para SQL Server".  
  
 A continuación se muestra un ejemplo del resultado de las llamadas a los métodos de la clase SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Donde "xxx.x" es el número de la versión final.  
  
## <a name="see-also"></a>Consulte también  
 [Diagnóstico de problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
