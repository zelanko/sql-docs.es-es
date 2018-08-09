---
title: Mejora del rendimiento y la confiabilidad del controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
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
ms.openlocfilehash: b9780fc2942f74df6eb26c5cccfad60821b9bfc0
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39459719"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>Mejorar el rendimiento y la confiabilidad con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Un aspecto del desarrollo de aplicaciones común a todas las aplicaciones es la necesidad constante de mejorar el rendimiento y la confiabilidad. Hay diversas técnicas para hacerlo con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
En los temas de esta sección se describen las distintas técnicas para aumentar el rendimiento y la confiabilidad de la aplicación al usar el controlador JDBC.  

## <a name="in-this-section"></a>En esta sección

|Tema|Descripción|  
|-----------|-----------------|  
|[Cerrar los objetos cuando no se usan](../../connect/jdbc/closing-objects-when-not-in-use.md)|Describe la importancia de cerrar los objetos del controlador JDBC cuando ya no son necesarios.|  
|[Administrar el tamaño de las transacciones](../../connect/jdbc/managing-transaction-size.md)|Describe las técnicas para aumentar el rendimiento de las transacciones.|  
|[Trabajar con instrucciones y conjuntos de resultados](../../connect/jdbc/working-with-statements-and-result-sets.md)|Describe técnicas para mejorar el rendimiento al utilizar los objetos de la instrucción o el conjunto de resultados.|  
|[Usar el almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md)|El controlador JDBC proporciona ahora una característica de almacenamiento en búfer adaptable, que se ha diseñado para recuperar cualquier tipo de datos de valores grandes sin tener que sufrir la sobrecarga de los cursores de servidor.|  
|[Columnas dispersas](../../connect/jdbc/sparse-columns.md)|En este tema se detalla la compatibilidad del controlador JDBC con las columnas dispersas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Almacenamiento en caché de metadatos de instrucción preparado para el controlador JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Describe las técnicas para mejorar el rendimiento con las consultas de la instrucción preparada.|
|[Uso de la API de copia masiva para la operación de inserción por lotes](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|Describe cómo habilitar la API de copia masiva para las operaciones de inserción por lotes y sus ventajas.|

## <a name="see-also"></a>Vea también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  