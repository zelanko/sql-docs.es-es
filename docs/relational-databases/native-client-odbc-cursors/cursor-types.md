---
description: Tipos de cursor
title: Tipos de cursor | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bffc8d5197117533913dca63c171fb4fffab588
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438660"
---
# <a name="cursor-types"></a>Tipos de cursor
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC define cuatro tipos de cursor compatibles con Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. Estos cursores varían en función de la capacidad de detectar cambios en el conjunto de resultados y en los recursos que consumen, como la memoria y el espacio en **tempdb**. Un cursor solamente puede detectar cambios en las filas cuando intenta volver a capturar estas filas; el origen de datos no dispone de ningún método para notificar al cursor los cambios en las filas actualmente capturadas. El nivel de aislamiento de transacción también afecta la capacidad de un cursor para detectar modificaciones que no se realizaron a través del cursor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite cuatro tipos de cursor ODBC:  
  
-   Los cursores de solo avance no admiten el desplazamiento; solo admiten la captura de filas en serie desde el inicio hasta el final del cursor.  
  
-   Los cursores estáticos se crean en **tempdb** cuando se abre el cursor. Siempre muestran el conjunto de resultados tal como estaba al abrir el cursor. Nunca reflejan los cambios en los datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores estáticos son siempre de solo lectura. Dado que un cursor de servidor estático se genera como una tabla de trabajo en **tempdb**, el tamaño del conjunto de resultados del cursor no puede superar el tamaño de fila máximo permitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   En los cursores controlados por conjunto de claves, la pertenencia y el orden de las filas del conjunto de resultados se fijan al abrir el cursor. Los cambios en las columnas sin clave son visibles a través del cursor.  
  
-   Los cursores dinámicos son los opuestos a los cursores estáticos. Reflejan todas las modificaciones realizadas en las filas de su conjunto de resultados. Los valores de datos, el orden y la pertenencia de las filas del conjunto de resultados pueden cambiar con cada captura.  
  
## <a name="see-also"></a>Consulte también  
 [Usar cursores &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
