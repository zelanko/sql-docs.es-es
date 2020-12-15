---
description: Datos en ejecución y columnas de tipo text, ntext o image
title: Datos en ejecución y Text, ntext, Image
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32f2bb59a0632c7070230750c720398a419b96b0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464926"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Datos en ejecución y columnas de tipo text, ntext o image
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Datos en ejecución de ODBC es una característica que habilita a las aplicaciones para trabajar con grandes volúmenes de datos en columnas o parámetros enlazados. Al recuperar columnas **Text**, **ntext** o **Image** muy grandes, es posible que una aplicación no pueda asignar simplemente un búfer enorme, enlazar la columna al búfer y capturar la fila. Al actualizar columnas **Text**, **ntext** o **Image** muy grandes, es posible que la aplicación no pueda asignar simplemente un búfer enorme, enlazarlo a un marcador de parámetro en una instrucción SQL y, a continuación, ejecutar la instrucción. En estos casos, la aplicación debe utilizar [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) con sus opciones de datos en ejecución.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
