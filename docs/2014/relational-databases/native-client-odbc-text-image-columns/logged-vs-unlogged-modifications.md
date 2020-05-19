---
title: Modificaciones registradas frente a no registradas | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3635fee71c92196cbc9408db1487e95da2b489ea
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718765"
---
# <a name="logged-vs-unlogged-modifications"></a>Modificaciones registradas frente a modificaciones no registradas
  Una aplicación puede solicitar que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no registre las modificaciones de **Text**, **ntext**e **Image** . Sin embargo, se debe tener cautela con esta opción. Solo se debe usar para aquellas situaciones en las que los datos **Text**, **ntext**o **Image** no son críticos y los propietarios de datos están dispuestos a deshacer la capacidad de recuperar datos para un mayor rendimiento.  
  
 El registro de las modificaciones de **Text**, **ntext**e **Image** se controla mediante una llamada a [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) con el parámetro de *atributo* establecido en SQL_SOPT_SS_ TEXTPTR_LOGGING y *ValuePtr* establecido en SQL_TL_ON o SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](managing-text-and-image-columns.md)  
  
  
