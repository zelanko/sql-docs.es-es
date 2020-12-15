---
description: Administrar columnas de texto e imagen
title: Administrar columnas de texto e imagen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c35d7bdbca8889f1cdd4d8f748ee8e9cae02d02
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469486"
---
# <a name="managing-text-and-image-columns"></a>Administrar columnas de texto e imagen
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los datos de tipo **Text**, **ntext** e **Image** (también denominados datos Long) son tipos de datos de cadenas binarias o de caracteres que pueden contener valores de datos demasiado grandes para caber en columnas **Char**, **VARCHAR**, **Binary** o **varbinary** . El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos de **texto** se asigna al tipo de datos SQL_LONGVARCHAR ODBC; **ntext** se asigna a SQL_WLONGVARCHAR; y los mapas de **imagen** para SQL_LONGVARBINARY. Es posible que algunos elementos de datos, como documentos largos o mapas de bits grandes, resulten demasiado grandes para poder almacenarlos correctamente en la memoria. Para recuperar datos largos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en partes secuenciales, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite que una aplicación llame a [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Para enviar datos largos en partes secuenciales, la aplicación puede llamar a [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). Los parámetros para los que se envían datos durante la ejecución se conocen como parámetros de datos en ejecución.  
  
 En realidad, una aplicación puede escribir o recuperar cualquier tipo de datos (no solo datos largos) con **SQLPutData** o **SQLGetData**, aunque solo los datos de **caracteres** y **binarios** se pueden enviar o recuperar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un solo búfer, generalmente no hay ningún motivo para usar **SQLPutData** o **SQLGetData**. Resulta mucho más fácil enlazar el búfer único al parámetro o columna.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Texto delimitado frente a texto sin delimitar y columnas de imagen](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificaciones registradas frente a modificaciones no registradas](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Datos en ejecución y columnas de tipo text, ntext o image](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
