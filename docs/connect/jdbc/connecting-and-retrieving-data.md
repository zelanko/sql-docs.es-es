---
title: Conectarse y recuperar datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 049b3cbc3a5ddebd30aa111f7c3bd62d46360f43
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-and-retrieving-data"></a>Conectar y recuperar datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se trabaja con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], hay dos métodos principales para establecer una conexión con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. Una consiste en establecer las propiedades de conexión en la dirección URL de conexión y, a continuación, llame al método getConnection de la clase DriverManager para devolver un [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
> [!NOTE]  
>  Para obtener una lista de las propiedades de conexión admitidas por el controlador JDBC, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 El segundo método implica el establecimiento de las propiedades de conexión mediante el uso de métodos de establecimiento de la [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) clase y, a continuación, llamar a la [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) método para devolver un SQLServerConnection objeto.  
  
 Los temas de esta sección describen las distintas maneras en que puede conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos y se muestran las distintas técnicas para recuperar datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Ejemplo de URL de conexión](../../connect/jdbc/connection-url-sample.md)|Describe cómo utilizar una dirección URL de conexión para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y, a continuación, usar una instrucción SQL para recuperar datos.|  
|[Ejemplo de origen de datos](../../connect/jdbc/data-source-sample.md)|Describe cómo usar un origen de datos para conectarse a SQL y usar un procedimiento almacenado para recuperar datos.|  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones del controlador JDBC de ejemplo](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
