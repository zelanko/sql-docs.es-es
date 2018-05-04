---
title: Mejora del rendimiento y confiabilidad con el controlador JDBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58521cbe6c21e7ef58fc97b52e1ef6b27209e4fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
|[Almacenamiento en caché de metadatos de instrucción preparado para el controlador JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Describe las técnicas para mejorar el rendimiento con las consultas de la instrucción preparada.|
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  