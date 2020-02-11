---
title: Columnas de imagen y texto enlazado frente a sin enlazar | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d23b999c40aaa6a7cd8200185f18f14ac759403f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73778873"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Texto delimitado y sin delimitar y columnas de imagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cuando se utilizan cursores de servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el controlador ODBC de Native Client está optimizado para no transmitir los datos para las columnas **Text**, **ntext**o **Image** sin enlazar en el momento en que se realiza el **SQLFetch** . Los datos **Text**, **ntext**o **Image** no se recuperan realmente del servidor hasta que la aplicación emite [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para la columna.  
  
 Se pueden escribir muchas aplicaciones para que no se muestren datos de **texto**, **ntext**o **Image** mientras un usuario simplemente se desplaza hacia arriba y hacia abajo en un cursor. Cuando un usuario selecciona una fila para obtener más detalles, la aplicación puede llamar a **SQLGetData** para recuperar los datos **Text**, **ntext**o **Image** . Esto evitará que se transmitan los datos **Text**, **ntext**o **Image** para cualquiera de las filas que el usuario no selecciona y, por tanto, puede evitar la transmisión de cantidades muy grandes de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamientos de los cursores](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
