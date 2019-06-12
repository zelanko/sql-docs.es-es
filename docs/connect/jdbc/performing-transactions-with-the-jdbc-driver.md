---
title: Realizar transacciones con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8471493fb68df8369084046075f88a1e7b4f2e3e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794094"
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>Realizar transacciones con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El procesamiento de transacciones es un requisito obligatorio para todas las aplicaciones que deban garantizar la coherencia de sus datos persistentes. Con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], el procesamiento de transacciones se puede realizar de forma local o distribuida. Las transacciones son módulos de ejecución atómicos, coherentes, aislados y durables (ACID).  
  
 Los temas de esta sección describen la forma en la que el controlador JDBC admite transacciones, incluyendo niveles de aislamiento, puntos de retorno de transacciones y capacidad de alojamiento del conjunto de resultados.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Descripción de transacciones](../../connect/jdbc/understanding-transactions.md)|Proporciona una introducción a la forma en la que se usan transacciones con el controlador JDBC.|  
|[Descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md)|Proporciona una introducción a la forma en la que se usan transacciones XA con el controlador JDBC.|  
|[Descripción de los niveles de aislamiento](../../connect/jdbc/understanding-isolation-levels.md)|Describe los diferentes niveles de aislamiento que admite el controlador JDBC.|  
|[Usar puntos de retorno](../../connect/jdbc/using-savepoints.md)|Describe cómo usar el controlador JDBC con puntos de retorno de transacciones.|  
|[Usar la capacidad de alojamiento](../../connect/jdbc/using-holdability.md)|Describe cómo usar el controlador JDBC con la capacidad de alojamiento del conjunto de resultados.|  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
