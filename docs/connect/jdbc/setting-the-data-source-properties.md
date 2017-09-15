---
title: "Propiedades del origen de configuración de los datos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e49d68f567f26e852dcf8bee3a9827797c9c23f2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-data-source-properties"></a>Establecer las propiedades de los orígenes de datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Los orígenes de datos son el mecanismo preferido por el que crear conexiones de JDBC en un entorno Java Platform, Enterprise Edition (Java EE). Los orígenes de datos proporcionan conexiones, conexiones agrupadas y conexiones distribuidas sin codificar de forma rígida las propiedades de la conexión en código Java. Todos los [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] orígenes de datos pueden establecer u obtener el valor de cualquier propiedad mediante los adecuados métodos establecedor y captador, respectivamente.  
  
 Los productos de Java EE, tales como servidores de aplicaciones y motores de servlet/JSP, normalmente le permiten configurar los orígenes de datos para el acceso a bases de datos. Todas las propiedades enumeradas en la [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) tema puede especificarse siempre que la configuración le permita escribir una propiedad como una propiedad = par de valor.  
  
 Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] orígenes de datos, vea el [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) clase. Para obtener un ejemplo de cómo utilizar la clase SQLServerDataSource para establecer una conexión con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] la base de datos, vea [ejemplo de origen de datos](../../connect/jdbc/data-source-sample.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
