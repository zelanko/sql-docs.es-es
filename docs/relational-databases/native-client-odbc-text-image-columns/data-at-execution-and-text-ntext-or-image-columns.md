---
title: Datos en ejecución y Text, ntext o Image Columns | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56cf9e564eb21d0036b61be0fde1404ed1dee486
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694636"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Datos en ejecución y columnas de tipo text, ntext o image
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Datos en ejecución de ODBC es una característica que habilita a las aplicaciones para trabajar con grandes volúmenes de datos en columnas o parámetros enlazados. Cuando se recuperan un gran **texto**, **ntext**, o **imagen** de las columnas, una aplicación no puede ser puede simplemente asignar un búfer enorme, enlazar la columna en el búfer y capturar la fila. Cuando se actualiza un gran **texto**, **ntext**, o **imagen** columnas, la aplicación no puede simplemente asignar un búfer enorme, enlazarlo a un marcador de parámetro en un SQL instrucción y, a continuación, ejecute la instrucción. En estos casos, la aplicación debe utilizar [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) con sus opciones de datos en ejecución.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
