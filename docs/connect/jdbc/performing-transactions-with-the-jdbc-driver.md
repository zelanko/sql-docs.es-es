---
title: Realizar transacciones con el controlador JDBC | Documentos de Microsoft
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
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cecc83cced06fcc53fcddaa365e5c04fedbf469
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>Realizar transacciones con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El procesamiento de transacciones es un requisito obligatorio para todas las aplicaciones que deban garantizar la coherencia de sus datos persistentes. Con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], procesamiento de transacciones puede realizar de forma local o distribuido. Las transacciones son módulos de ejecución atómicos, coherentes, aislados y durables (ACID).  
  
 Los temas de esta sección describen la forma en la que el controlador JDBC admite transacciones, incluyendo niveles de aislamiento, puntos de retorno de transacciones y capacidad de alojamiento del conjunto de resultados.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Descripción de transacciones](../../connect/jdbc/understanding-transactions.md)|Proporciona una introducción a la forma en la que se usan transacciones con el controlador JDBC.|  
|[Descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md)|Proporciona una introducción a la forma en la que se usan transacciones XA con el controlador JDBC.|  
|[Descripción de los niveles de aislamiento](../../connect/jdbc/understanding-isolation-levels.md)|Describe los diferentes niveles de aislamiento que admite el controlador JDBC.|  
|[Usar puntos de retorno](../../connect/jdbc/using-savepoints.md)|Describe cómo usar el controlador JDBC con puntos de retorno de transacciones.|  
|[Usar la capacidad de alojamiento](../../connect/jdbc/using-holdability.md)|Describe cómo usar el controlador JDBC con la capacidad de alojamiento del conjunto de resultados.|  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
