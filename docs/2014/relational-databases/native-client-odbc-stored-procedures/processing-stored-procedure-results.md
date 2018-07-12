---
title: Procesar resultados del procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 767eb56845429a19575d1339976a014ec3ea5288
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411034"
---
# <a name="processing-stored-procedure-results"></a>Procesar resultados de procedimientos almacenados
  Los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen cuatro mecanismos que se utilizan para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   Un parámetro de salida del cursor puede devolver un cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 Las aplicaciones deben ser capaces de administrar todos estos resultados de los procedimientos almacenados. La instrucción CALL o EXECUTE debería incluir los marcadores de parámetros para el código de retorno y los parámetros de salida. Use [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) para enlazarlos todos como parámetros de salida y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client transferirá los valores de salida a las variables enlazadas. Parámetros de salida y devolver los códigos son los últimos elementos que se devuelve al cliente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no se devuelven a la aplicación hasta que [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) devuelve SQL_NO_DATA.  
  
 ODBC no permite enlazar parámetros de cursor [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puesto que todos los parámetros de salida se deben enlazar antes de ejecutar un procedimiento, las aplicaciones ODBC no pueden llamar a ningún procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenga un parámetro de cursor de salida.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar procedimientos almacenados](running-stored-procedures.md)  
  
  
