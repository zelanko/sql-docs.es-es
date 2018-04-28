---
title: Usar instrucciones con SQL | Documentos de Microsoft
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
ms.topic: article
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 361448b1b27a735f54202a3ec6bbbec8f16ccc72
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-statements-with-sql"></a>Usar instrucciones con SQL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se trabaja con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e instrucciones SQL insertadas, varias clases que puede utilizar. La clase usada depende del tipo de instrucción SQL que desee ejecutar.  
  
 Si la instrucción SQL no contiene parámetros IN, use la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase, pero si contiene parámetros IN, use la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase.  
  
> [!NOTE]  
>  Si necesita usar instrucciones SQL que contengan IN y parámetros OUT, debe implementarlos como un procedimiento almacenado y llamarlo con la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase. Para obtener más información sobre el uso de procedimientos almacenados, vea [instrucciones Using con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
 Las siguientes secciones describen los escenarios diferentes para trabajar con datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante instrucciones SQL.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Usar una instrucción SQL sin parámetros](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|Describe cómo usar instrucciones SQL que no contienen parámetros.|  
|[Usar una instrucción SQL con parámetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|Describe cómo usar instrucciones SQL que contienen parámetros.|  
|[Usar una instrucción SQL para modificar objetos de la base de datos](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|Describe cómo usar instrucciones SQL para modificar objetos de la base de datos.|  
|[Usar una instrucción SQL para modificar datos](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|Describe cómo usar instrucciones SQL para modificar datos de una base de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
