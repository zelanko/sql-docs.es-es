---
title: Trabajar con conjuntos de resultados | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db287cf250687be6f484646ec706cc015028e3ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-result-sets"></a>Trabajar con conjuntos de resultados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cuando se trabaja con los datos contenidos en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos, un método de manipular los datos consiste en utilizar un conjunto de resultados. El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] admite el uso del resultado se establece a través de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto. Utilizando el objeto SQLServerResultSet, puede recuperar los datos devueltos por una instrucción SQL o procedimiento almacenado, actualizar los datos según sea necesario y, a continuación, volver a almacenar datos en la base de datos.  
  
 Además, el objeto SQLServerResultSet proporciona métodos para desplazarse por las filas de datos, obtener o establecer los datos que contiene y para establecer varios niveles de sensibilidad a los cambios en la base de datos subyacente.  
  
> [!NOTE]  
>  Para obtener más información acerca de cómo administrar los conjuntos de resultados, incluida la sensibilidad a los cambios, consulte [administrar conjuntos de resultados con el controlador JDBC](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
 Los temas de esta sección describen distintas formas que puede usar un conjunto de resultados para manipular los datos contenidos en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Recuperación de ejemplos de datos de conjunto de resultados](../../../connect/jdbc/retrieving-result-set-data-sample.md)|Describe cómo usar un conjunto de resultados para recuperar los datos de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] la base de datos y mostrarlos.|  
|[Modificación de ejemplos de datos de conjunto de resultados](../../../connect/jdbc/modifying-result-set-data-sample.md)|Describe cómo usar un conjunto de resultados para insertar, recuperar y modificar datos en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.|  
|[Almacenamiento en caché de ejemplos de datos de conjunto de resultados](../../../connect/jdbc/caching-result-set-data-sample.md)|Describe cómo usar un conjunto de resultados para recuperar grandes cantidades de datos de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos y para controlar cómo se almacena en caché los datos en el cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones del controlador JDBC de ejemplo](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
