---
title: Compatibilidad entre versiones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7990072ac539addf733720fd8c1eaba0652f5d70
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304519"
---
# <a name="cross-version-compatibility"></a>Compatibilidad entre versiones
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Pueden producirse conflictos entre versiones cuando se espera que las instancias cliente o servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] procesen los parámetros con valores de tabla.  
  
 En general, la funcionalidad de los parámetros con valores de tabla solo está disponible para los clientes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (con SQL Server Native Client 10.0) o posterior que están conectados a los servidores de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior). Las nuevas columnas de los conjuntos de resultados de la función de catálogo solo estarán [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] presentes cuando se conecten a un servidor de (o posterior).  
  
 Si una aplicación cliente compilada con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ejecuta instrucciones que esperan parámetros con valores de tabla, el servidor detecta esta condición a través de un error de conversión de datos y ODBC devuelve esto como SQLSTATE 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".  
  
 Si una aplicación cliente que se compiló con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10,0 o una versión posterior intenta usar parámetros con valores de tabla cuando se conecta a una instancia [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servidor anterior a, Native Client lo detectará, y se producirá un error 07006 en las llamadas de tipo de datos restringido (la versión de SQL Server para esta conexión no admite parámetros con valores de tabla) ".  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
