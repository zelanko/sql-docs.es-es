---
title: Temas "Cómo..." de rendimiento de controlador ODBC (ODBC) de generación de perfiles | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9aa6ff562bc4a9b9f17d9527e156f1b2c03e4ea9
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426074"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>Generación de perfiles de rendimiento del controlador ODBC (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye dos opciones específicas del controlador para generar perfiles de rendimiento del controlador.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC puede registrar las estadísticas de rendimiento en el archivo. El archivo de registro es un archivo delimitado por tabuladores que puede analizarse en cualquier hoja de cálculo que admita archivos delimitados por tabuladores, como Microsoft Excel.  
  
 El controlador también puede registrar consultas de ejecución prolongada (consultas que no reciben ninguna respuesta del servidor durante un intervalo de tiempo especificado). Los programadores y administradores de bases de datos pueden analizar después estas consultas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Generar perfiles de datos de rendimiento del controlador &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [Registrar consultas de larga ejecución &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>Vea también  
 [Temas de procedimientos de ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
