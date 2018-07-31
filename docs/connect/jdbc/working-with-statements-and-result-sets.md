---
title: Trabajar con instrucciones y conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14a6f86b503cf4c0f864a881479a37314c11d528
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37980486"
---
# <a name="working-with-statements-and-result-sets"></a>Trabajar con instrucciones y conjuntos de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Si trabaja con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] y los objetos Statement y ResultSet que proporciona, hay varias técnicas que puede usar para mejorar el rendimiento y la confiabilidad de las aplicaciones.  
  
## <a name="use-the-appropriate-statement-object"></a>Usar un objeto de instrucción correcto  
 Si usa uno de los objetos Statement del controlador JDBC, como [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), asegúrese de que está usando el objeto correcto para el trabajo.  
  
-   Si no tiene parámetros OUT, no es necesario utilizar el objeto SQLServerCallableStatement. En su lugar, use SQLServerStatement o el objeto SQLServerPreparedStatement.  
  
-   Si no va a ejecutar la instrucción más de una vez o no tiene IN o los parámetros OUT, no es necesario utilizar el objeto SQLServerPreparedStatement o SQLServerCallableStatement. En su lugar, use el objeto SQLServerStatement.  
  
## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>Usar la simultaneidad correcta para los objetos ResultSet  
 No solicite una simultaneidad actualizable si va a crear instrucciones que generan conjuntos de resultados a menos que desee actualizar los resultados. El modelo de cursor predeterminado de solo avance y solo lectura es el método más rápido para leer conjuntos de resultados pequeños.  
  
## <a name="limit-the-size-of-your-result-sets"></a>Limitar el tamaño de los conjuntos de resultados  
 Considere la posibilidad de usar el método [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) (o la sintaxis SET ROWCOUNT o SELECT TOP N SQL) para limitar el número de filas devueltas por conjuntos de resultados posiblemente grandes. Si es necesario administrar conjuntos de resultados grandes, considere la posibilidad de usar almacenamiento en búfer de respuesta adaptable configurando la propiedad de cadena de conexión responseBuffering=adaptive, que es el modo predeterminado. Este enfoque permite a la aplicación procesar conjuntos de resultados grandes sin requerir los cursores del lado del servidor, minimizando el uso de memoria de la aplicación. Para obtener más información, consulte [usando almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="use-the-appropriate-fetch-size"></a>Usar el tamaño de captura correcto  
 En el caso de los cursores de servidor de solo lectura, el inconveniente son los ciclos de ida y vuelta al servidor frente a la cantidad de memoria usada en el controlador. Para los cursores de servidor actualizables, el tamaño de captura también influye en la sensibilidad del conjunto de resultados frente a los cambios y en la simultaneidad en el servidor. Las actualizaciones de las filas en el búfer de captura actual no son visibles hasta que se genera un método [refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) explícito o hasta que el cursor sale del búfer de recuperación. Los búferes de captura grandes ofrecen un mayor rendimiento (menos ciclos de ida y vuelta del servidor), pero son menos sensibles a los cambios y reducen la simultaneidad del servidor si se usa CONCUR_SS_SCROLL_LOCKS (1009). Para obtener el máximo nivel de sensibilidad a los cambios, use un tamaño de captura de 1. No obstante, debe tener en cuenta que esto implica un ciclo de ida y vuelta en el servidor para cada fila recuperada.  
  
## <a name="use-streams-for-large-in-parameters"></a>Usar secuencias para parámetros IN grandes  
 Use secuencias o BLOB y CLOB materializados de forma incremental para controlar la actualización de valores de columnas grandes o el envío de parámetros IN grandes. El controlador JDBC los "fragmenta" en el servidor en varios ciclos de ida y vuelta, lo que permite establecer y actualizar valores mayores que los que puede contener la memoria.  
  
## <a name="see-also"></a>Ver también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
