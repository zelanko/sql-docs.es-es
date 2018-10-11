---
title: Obtener la versión del controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7abc69edd0d49264a62ea0c3f65a60b58549d105
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774223"
---
# <a name="getting-the-driver-version"></a>Obtener la versión del controlador
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  La versión del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] instalado se puede encontrar de las maneras siguientes:  
  
-   Llame a los métodos [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) o [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   La versión se muestra en el archivo readme.txt de la distribución del producto.  
  
 Además, el nombre del controlador JDBC se puede devolver desde la llamada al método [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) de la clase SQLServerDatabaseMetaData. Devolverá, por ejemplo, "Controlador Microsoft JDBC 6.4 para SQL Server".  
  
 El siguiente es un ejemplo de la salida de las llamadas a los métodos de la clase SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Donde "xxx.x" es el número de la versión final.  
  
## <a name="see-also"></a>Ver también  
 [Diagnosticar problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
