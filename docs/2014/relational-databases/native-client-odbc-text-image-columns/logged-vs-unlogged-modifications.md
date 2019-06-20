---
title: Modificaciones registradas frente a No registradas modificaciones | Microsoft Docs
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
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c722d5360ad01e7e95508c2219ceb674de381286
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63195136"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificaciones registradas frente a modificaciones no registradas
  Una aplicación puede solicitar que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no registro **texto**, **ntext**, y **imagen** modificaciones. Sin embargo, se debe tener cautela con esta opción. Debe usarse solo en aquellas situaciones donde la **texto**, **ntext**, o **imagen** datos no son fundamentales y propietarios de los datos están dispuestos a compensar la capacidad para recuperar datos un mayor rendimiento.  
  
 El registro de **texto**, **ntext**, y **imagen** modificaciones se controla mediante una llamada a [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) con el  *Atributo* parámetro establecido en SQL_SOPT_SS_ TEXTPTR_LOGGING y *ValuePtr* establecido en SQL_TL_ON o SQL_TL_OFF.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas de texto e imagen](managing-text-and-image-columns.md)  
  
  
