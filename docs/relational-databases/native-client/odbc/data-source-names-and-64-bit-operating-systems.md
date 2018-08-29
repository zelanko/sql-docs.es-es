---
title: Los nombres y los sistemas operativos de 64 bits de origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24af2f7d0d6feae7a7c4ab6c6e6635cb281f1ba0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43098751"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nombres de origen de datos y sistemas operativos de 64 bits
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Para generar y ejecutar una aplicación como una aplicación de 32 bits en un sistema operativo de 64 bits, debe crear el origen de datos ODBC con el Administrador de ODBC de %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Notas  
 Un sistema operativo Windows de 64 bits tiene dos archivos odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe se usa para crear y mantener nombres de origen de datos para las aplicaciones de 64 bits.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe se usa crear y mantener nombres de origen de datos para las aplicaciones de 32 bits, incluso las aplicaciones de 32 bits que se ejecutan en sistemas operativos de 64 bits.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
