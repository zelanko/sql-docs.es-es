---
title: Administración de columnas de texto e imagen ? Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3ac58e59f66dd107a9523a42f5647c90b4fb737
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297725"
---
# <a name="managing-text-and-image-columns"></a>Administrar columnas de texto e imagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**los**datos text , **ntext**e **image** (también denominados datos largos) son tipos de datos de caracteres o cadenas binarias que pueden contener valores de datos demasiado grandes para caber en columnas **char**, **varchar**, **binary**o **varbinary.** El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos de **texto** se asigna al tipo de datos odbc SQL_LONGVARCHAR; **ntext** se asigna a SQL_WLONGVARCHAR; y mapas de **imágenes** para SQL_LONGVARBINARY. Es posible que algunos elementos de datos, como documentos largos o mapas de bits grandes, resulten demasiado grandes para poder almacenarlos correctamente en la memoria. Para recuperar datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] largos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] partes secuenciales, el controlador ODBC de Native Client permite que una aplicación llame a [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Para enviar datos largos en partes secuenciales, la aplicación puede llamar a [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). Los parámetros para los que se envían datos durante la ejecución se conocen como parámetros de datos en ejecución.  
  
 Una aplicación realmente puede escribir o recuperar cualquier tipo de datos (no solo datos largos) con **SQLPutData** o **SQLGetData**, aunque solo se pueden enviar o recuperar datos **binarios** y **de caracteres** en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, generalmente no hay ninguna razón para usar **SQLPutData** o **SQLGetData**. Resulta mucho más fácil enlazar el búfer único al parámetro o columna.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Texto delimitado frente a texto sin delimitar y columnas de imagen](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificaciones registradas frente a modificaciones no registradas](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Datos en ejecución y columnas de tipo text, ntext o image](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
