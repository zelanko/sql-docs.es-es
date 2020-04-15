---
title: Compatibilidad entre versiones de la versión de la versión de la versión de la versión Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304519"
---
# <a name="cross-version-compatibility"></a>Compatibilidad entre versiones
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Pueden producirse conflictos entre versiones cuando se espera que las instancias cliente o servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] procesen los parámetros con valores de tabla.  
  
 En general, la funcionalidad de los parámetros con valores de tabla solo está disponible para los clientes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (con SQL Server Native Client 10.0) o posterior que están conectados a los servidores de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior). Las nuevas columnas de los conjuntos de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] resultados de funciones de catálogo solo estarán presentes cuando estén conectadas a un servidor (o posterior).  
  
 Si una aplicación cliente compilada con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ejecuta instrucciones que esperan parámetros con valores de tabla, el servidor detecta esta condición a través de un error de conversión de datos y ODBC devuelve esto como SQLSTATE 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".  
  
 Si una aplicación cliente que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se compiló con Native Client 10.0 o posterior intenta usar [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]parámetros con valores de tabla cuando se conecta a una instancia de servidor anterior a , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client detectará esto y SQLBindCol, SQLBindParameter, SQLSetDescFields, y SQLSetDescRec llamadas producirá un error con SQLSTATE 07006 y el mensaje "Atributo de infracción de tipo de datos restringidos (la versión de SQL Server para esta conexión no admite parámetros con valores de tabla)".  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
