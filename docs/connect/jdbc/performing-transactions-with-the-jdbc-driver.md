---
title: Transacciones con el controlador JDBC
description: Obtenga información sobre cómo el controlador JDBC para SQL Server admite transacciones, incluyendo niveles de aislamiento, puntos de retorno y capacidad de alojamiento del conjunto de resultados.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff851fc3d62be939eab7983eee80a173160f0d5c
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435408"
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>Transacciones con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El procesamiento de transacciones es un requisito obligatorio para todas las aplicaciones que deban garantizar la coherencia de sus datos persistentes. Con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], el procesamiento de transacciones se puede realizar de forma local o distribuida. Las transacciones son módulos de ejecución atómicos, coherentes, aislados y durables (ACID).  
  
 Los temas de esta sección describen la forma en la que el controlador JDBC admite transacciones, incluyendo niveles de aislamiento, puntos de retorno de transacciones y capacidad de alojamiento del conjunto de resultados.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Descripción de las transacciones](../../connect/jdbc/understanding-transactions.md)|Proporciona una introducción a la forma en la que se usan transacciones con el controlador JDBC.|  
|[Descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md)|Proporciona una introducción a la forma en la que se usan transacciones XA con el controlador JDBC.|  
|[Descripción de los niveles de aislamiento](../../connect/jdbc/understanding-isolation-levels.md)|Describe los diferentes niveles de aislamiento que admite el controlador JDBC.|  
|[Empleo de puntos de retorno](../../connect/jdbc/using-savepoints.md)|Describe cómo usar el controlador JDBC con puntos de retorno de transacciones.|  
|[Empleo de la capacidad de alojamiento](../../connect/jdbc/using-holdability.md)|Describe cómo usar el controlador JDBC con la capacidad de alojamiento del conjunto de resultados.|  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
