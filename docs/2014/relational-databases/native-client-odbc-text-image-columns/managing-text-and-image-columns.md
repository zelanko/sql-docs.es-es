---
title: Administrar columnas de texto e imagen | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e6f790a82b45f9a74318a8ec46ef1e4f2a283edb
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709284"
---
# <a name="managing-text-and-image-columns"></a>Administrar columnas de texto e imagen
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los datos de tipo **Text**, **ntext**e **Image** (también denominados datos Long) son tipos de datos de cadenas binarias o de caracteres que pueden contener valores de datos demasiado grandes para caber en columnas **Char**, **VARCHAR**, **Binary**o **varbinary** . El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos de **texto** se asigna al tipo de datos SQL_LONGVARCHAR ODBC; **ntext** se asigna a SQL_WLONGVARCHAR; y los mapas de **imagen** para SQL_LONGVARBINARY. Es posible que algunos elementos de datos, como documentos largos o mapas de bits grandes, resulten demasiado grandes para poder almacenarlos correctamente en la memoria. Para recuperar datos largos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en partes secuenciales, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite que una aplicación llame a [SQLGetData](../native-client-odbc-api/sqlgetdata.md). Para enviar datos largos en partes secuenciales, la aplicación puede llamar a [SQLPutData](../native-client-odbc-api/sqlputdata.md). Los parámetros para los que se envían datos durante la ejecución se conocen como parámetros de datos en ejecución.  
  
 En realidad, una aplicación puede escribir o recuperar cualquier tipo de datos (no solo datos largos) con **SQLPutData** o **SQLGetData**, aunque solo los datos de **caracteres** y **binarios** se pueden enviar o recuperar en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un solo búfer, generalmente no hay ningún motivo para usar **SQLPutData** o **SQLGetData**. Resulta mucho más fácil enlazar el búfer único al parámetro o columna.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Texto delimitado frente a texto sin delimitar y columnas de imagen](bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificaciones registradas frente a modificaciones no registradas](logged-vs-unlogged-modifications.md)  
  
-   [Datos en ejecución y columnas de tipo text, ntext o image](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
