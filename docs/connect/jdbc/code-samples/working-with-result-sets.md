---
title: Trabajar con conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b5c2df6c7c932e16394b91e76719756d9b959ff
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39458469"
---
# <a name="working-with-result-sets"></a>Trabajar con conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Si trabaja con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], uno de los métodos para manipular los datos consiste en usar un conjunto de resultados. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] admite el uso de conjuntos de resultados mediante el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Si usa el objeto SQLServerResultSet, puede recuperar los datos devueltos desde una instrucción SQL o un procedimiento almacenado, actualizar los datos según sea necesario y luego volver a almacenarlos en la base de datos.  
  
Además, el objeto SQLServerResultSet proporciona métodos para desplazarse por las filas de datos, obtener o configurar los datos que contiene y establecer varios niveles de sensibilidad a los cambios en la base de datos subyacente.  
  
> [!NOTE]  
> Para obtener más información acerca de cómo administrar conjuntos de resultados, incluida la sensibilidad a los cambios, consulte [administrar conjuntos de resultados con el controlador JDBC](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
En los temas de esta sección se describen las distintas formas en que puede usar un conjunto de resultados para manipular los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                                           | Descripción                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Recuperación de ejemplos de datos de conjunto de resultados](../../../connect/jdbc/code-samples/retrieving-result-set-data-sample.md) | Se describe cómo usar un conjunto de resultados para recuperar y mostrar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].                                                         |
| [Modificación de ejemplos de datos de conjunto de resultados](../../../connect/jdbc/code-samples/modifying-result-set-data-sample.md)   | Se describe cómo usar un conjunto de resultados para insertar, recuperar y modificar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].                                                      |
| [Almacenamiento en caché de ejemplos de datos de conjunto de resultados](../../../connect/jdbc/code-samples/caching-result-set-data-sample.md)       | Se describe cómo usar un conjunto de resultados para recuperar grandes cantidades de datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] y cómo controlar el modo en que los datos se almacenan en la memoria caché del cliente. |
  
## <a name="see-also"></a>Ver también  

[Aplicaciones del controlador JDBC de ejemplo](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  