---
title: Mejora del rendimiento y confiabilidad con el controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8b2d716ada4cb786eb141c0f49dcad41c5231c4
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>Mejorar el rendimiento y la confiabilidad con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Un aspecto del desarrollo de aplicaciones común a todas las aplicaciones es la necesidad constante de mejorar el rendimiento y la confiabilidad. Hay una serie de técnicas para hacerlo con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 En los temas de esta sección se describen las distintas técnicas para aumentar el rendimiento y la confiabilidad de la aplicación al usar el controlador JDBC.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Cerrar los objetos cuando no se usan](../../connect/jdbc/closing-objects-when-not-in-use.md)|Describe la importancia de cerrar los objetos del controlador JDBC cuando ya no son necesarios.|  
|[Administrar el tamaño de las transacciones](../../connect/jdbc/managing-transaction-size.md)|Describe las técnicas para aumentar el rendimiento de las transacciones.|  
|[Trabajar con instrucciones y conjuntos de resultados](../../connect/jdbc/working-with-statements-and-result-sets.md)|Describe técnicas para aumentar el rendimiento al usar los objetos de la instrucción o conjunto de resultados.|  
|[Usar el almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md)|El controlador JDBC proporciona ahora una característica de almacenamiento en búfer adaptable, que se ha diseñado para recuperar cualquier tipo de datos de valores grandes sin tener que sufrir la sobrecarga de los cursores de servidor.|  
|[Columnas dispersas](../../connect/jdbc/sparse-columns.md)|Explica la compatibilidad del controlador JDBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] columnas dispersas.|  
|[Almacenamiento en caché para el controlador JDBC de metadatos de instrucción preparada](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Describe las técnicas para mejorar el rendimiento con las consultas de la instrucción preparada.|
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  