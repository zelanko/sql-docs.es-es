---
description: Texto delimitado frente a texto sin delimitar y columnas de imagen
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 013e32489ba396f37260e5e614c4a21205d9f403
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88382501"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Texto delimitado frente a texto sin delimitar y columnas de imagen
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cuando se utilizan cursores de servidor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client está optimizado para no transmitir los datos para las columnas **Text**, **ntext**o **Image** sin enlazar en el momento en que se realiza el **SQLFetch** . Los datos **Text**, **ntext**o **Image** no se recuperan realmente del servidor hasta que la aplicación emite [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para la columna.  
  
 Se pueden escribir muchas aplicaciones para que no se muestren datos de **texto**, **ntext**o **Image** mientras un usuario simplemente se desplaza hacia arriba y hacia abajo en un cursor. Cuando un usuario selecciona una fila para obtener más detalles, la aplicación puede llamar a **SQLGetData** para recuperar los datos **Text**, **ntext**o **Image** . Esto evitará que se transmitan los datos **Text**, **ntext**o **Image** para cualquiera de las filas que el usuario no selecciona y, por tanto, puede evitar la transmisión de cantidades muy grandes de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamientos de los cursores](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
