---
title: Tipos de cursor | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 437b2d21e6441c3c6f6d94291d3f25d8546ddec4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134080"
---
# <a name="cursor-types"></a>Tipos de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC define cuatro tipos de cursor compatibles con Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. Estos cursores varían en su capacidad para detectar cambios en el conjunto de resultados y en los recursos que consumen, como la memoria y espacio en **tempdb**. Un cursor solamente puede detectar cambios en las filas cuando intenta volver a capturar estas filas; el origen de datos no dispone de ningún método para notificar al cursor los cambios en las filas actualmente capturadas. El nivel de aislamiento de transacción también afecta la capacidad de un cursor para detectar modificaciones que no se realizaron a través del cursor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite cuatro tipos de cursor ODBC:  
  
-   Los cursores de solo avance no admiten el desplazamiento; solo admiten la captura de filas en serie desde el inicio hasta el final del cursor.  
  
-   Los cursores estáticos se compilan **tempdb** cuando el cursor está abierto. Siempre muestran el conjunto de resultados tal como estaba al abrir el cursor. Nunca reflejan los cambios en los datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores estáticos son siempre de solo lectura. Dado que un cursor de servidor estático se genera como una tabla de trabajo en **tempdb**, el tamaño del conjunto de resultados del cursor no puede superar el tamaño de fila máximo permitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   En los cursores controlados por conjunto de claves, la pertenencia y el orden de las filas del conjunto de resultados se fijan al abrir el cursor. Los cambios en las columnas sin clave son visibles a través del cursor.  
  
-   Los cursores dinámicos son los opuestos a los cursores estáticos. Reflejan todas las modificaciones realizadas en las filas de su conjunto de resultados. Los valores de datos, el orden y la pertenencia de las filas del conjunto de resultados pueden cambiar con cada captura.  
  
## <a name="see-also"></a>Vea también  
 [Uso de cursores &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
