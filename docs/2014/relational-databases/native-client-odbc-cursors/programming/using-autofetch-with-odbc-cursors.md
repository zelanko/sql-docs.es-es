---
title: Usar la captura automática con cursores ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 177de8fe974d3aa4970f21607693a73c3da0b70e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104016"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Usar la captura automática con cursores ODBC
  Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite una opción de captura automática cuando se utiliza cualquier tipo de cursor de servidor. Con la captura automática, el **SQLExecute** o **SQLExecDirect** función que se abre el cursor también tiene un modo implícito [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)(función) (SQL_FIRST). Las filas que componen el primer conjunto de filas se devuelven a las variables de aplicación enlazadas como parte de la ejecución de la instrucción y se ahorra un viaje de ida y vuelta (round trip) de la red al servidor. [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) no se admite cuando la opción de recopilación automática está habilitada; se deben enlazar las columnas del conjunto de resultados a variables de programa.  
  
 Las aplicaciones solicitan la captura automática estableciendo el atributo de la instrucción SQL_SOPT_SS_CURSOR_OPTIONS específica del controlador en SQL_CO_AF.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de la programación de cursor &#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  