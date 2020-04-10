---
title: Mejora del rendimiento y la confiabilidad con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b82c2758dbc796ec29dd7304ee821a1a018af0a8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920735"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>Mejora del rendimiento y la confiabilidad con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Un aspecto del desarrollo de aplicaciones común a todas las aplicaciones es la necesidad constante de mejorar el rendimiento y la confiabilidad. Hay diversas técnicas para hacerlo con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
En los temas de esta sección se describen las distintas técnicas para aumentar el rendimiento y la confiabilidad de la aplicación al usar el controlador JDBC.  

## <a name="in-this-section"></a>En esta sección

|Tema|Descripción|  
|-----------|-----------------|  
|[Cierre de objetos cuando no se usan](../../connect/jdbc/closing-objects-when-not-in-use.md)|Describe la importancia de cerrar los objetos del controlador JDBC cuando ya no son necesarios.|  
|[Administración del tamaño de las transacciones](../../connect/jdbc/managing-transaction-size.md)|Describe las técnicas para aumentar el rendimiento de las transacciones.|  
|[Trabajo con instrucciones y conjuntos de resultados](../../connect/jdbc/working-with-statements-and-result-sets.md)|Describe las técnicas para aumentar el rendimiento al usar los objetos Statement o ResultSet.|  
|[Empleo de almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md)|El controlador JDBC proporciona ahora una característica de almacenamiento en búfer adaptable, que se ha diseñado para recuperar cualquier tipo de datos de valores grandes sin tener que sufrir la sobrecarga de los cursores de servidor.|  
|[Columnas dispersas](../../connect/jdbc/sparse-columns.md)|En este tema se detalla la compatibilidad del controlador JDBC con las columnas dispersas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Almacenamiento en caché de metadatos de instrucciones preparadas para el controlador JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Describe las técnicas para aumentar el rendimiento con consultas de instrucciones preparadas.|
|[Uso de la API de copia masiva para la operación de inserción por lotes](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|Describe cómo habilitar la API de copia masiva para las operaciones de inserción por lotes y sus ventajas.|

## <a name="see-also"></a>Consulte también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
