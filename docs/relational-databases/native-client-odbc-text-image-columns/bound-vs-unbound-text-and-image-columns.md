---
title: Columnas de texto y de imagen sin enlazar . Microsoft Docs
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
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cfa05f7019342d63ab6f3092c3b6df5ae6e8daa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297749"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Texto delimitado frente a texto sin delimitar y columnas de imagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilizan cursores de servidor, el controlador ODBC de Native Client está optimizado para no transmitir los datos de las columnas de **texto**sin enlazar, **ntext**o **imagen** en el momento en que se realiza **SQLFetch.** Los datos **text**, **ntext**o **image** no se recuperan realmente del servidor hasta que la aplicación emite [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para la columna.  
  
 Muchas aplicaciones se pueden escribir para que no se muestre ningún **texto,** **ntext**o datos de **imagen** mientras un usuario simplemente se desplaza hacia arriba y hacia abajo en un cursor. Cuando un usuario selecciona una fila para obtener más detalles, la aplicación puede llamar a **SQLGetData** para recuperar los datos de **texto,** **ntext**o **imagen.** Esto evitará la transmisión de los datos de **texto,** **ntext**o **imagen** para cualquiera de las filas que el usuario no selecciona y, por lo tanto, puede impedir la transmisión de grandes cantidades de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Administración de columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamientos de los cursores](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
