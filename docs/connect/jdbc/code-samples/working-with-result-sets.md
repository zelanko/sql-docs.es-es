---
title: Trabajar con conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44eac2fbcc156b3591bdf02fd00ff0d6bd19366b
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028244"
---
# <a name="working-with-result-sets"></a>Trabajo con conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Si trabaja con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uno de los métodos para manipular los datos consiste en usar un conjunto de resultados. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] admite el uso de conjuntos de resultados mediante el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Si usa el objeto SQLServerResultSet, puede recuperar los datos devueltos desde una instrucción SQL o un procedimiento almacenado, actualizar los datos según sea necesario y luego volver a almacenarlos en la base de datos.  
  
Además, el objeto SQLServerResultSet proporciona métodos para desplazarse por las filas de datos, obtener o configurar los datos que contiene y establecer varios niveles de sensibilidad a los cambios en la base de datos subyacente.  
  
> [!NOTE]  
> Para obtener más información sobre la administración de conjuntos de resultados, incluida la sensibilidad a los cambios, vea [administrar conjuntos de resultados con el controlador JDBC](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
En los temas de esta sección se describen las distintas formas en que puede usar un conjunto de resultados para manipular los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                                           | Descripción                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Recuperación de ejemplo de datos de conjunto de resultados](../../../connect/jdbc/code-samples/retrieving-result-set-data-sample.md) | Se describe cómo usar un conjunto de resultados para recuperar y mostrar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].                                                         |
| [Modificación de ejemplo de datos de conjunto de resultados](../../../connect/jdbc/code-samples/modifying-result-set-data-sample.md)   | Se describe cómo usar un conjunto de resultados para insertar, recuperar y modificar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].                                                      |
| [Almacenamiento en caché de ejemplo de datos de conjunto de resultados](../../../connect/jdbc/code-samples/caching-result-set-data-sample.md)       | Se describe cómo usar un conjunto de resultados para recuperar grandes cantidades de datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y cómo controlar el modo en que los datos se almacenan en la memoria caché del cliente. |
  
## <a name="see-also"></a>Vea también  

[Aplicaciones de ejemplo del controlador JDBC](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  
