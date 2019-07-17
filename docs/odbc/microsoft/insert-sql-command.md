---
title: 'Insertar: comando SQL | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 884a33339db10ee8e07d8b432d1765720d45734a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019451"
---
# <a name="insert---sql-command"></a>Insertar: comando SQL
Anexa un registro al final de una tabla que contiene los valores del campo especificado.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativa para este comando. Para obtener información específica del controlador, vea la sección Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argumentos  
 INSERT INTO *dbf_name*  
 Especifica el nombre de la tabla a la que se anexa el nuevo registro. *dbf_name* puede incluir una ruta de acceso y puede ser una expresión de nombre.  
  
 Si la tabla que especifique no está abierta, se abrirá exclusivamente en una nueva área de trabajo y el nuevo registro se anexa a la tabla. La nueva área de trabajo no está seleccionado; el área de trabajo actual permanece seleccionado.  
  
 Si la tabla que se especifique está abierta, INSERT anexa el nuevo registro a la tabla. Si la tabla está abierta en un área de trabajo distintos de área de trabajo actual, no está seleccionada una vez que se anexa el registro; el área de trabajo actual permanece seleccionado.  
  
 [( *fname1*[, *fname2*[,...]])]  
 Especifica en el nuevo registro de los nombres de los campos en que se insertan los valores.  
  
 VALORES ( *eExpression1*[, *eExpression2*[,...]])  
 Especifica los valores de campo que se inserta en el nuevo registro. Si omite los nombres de campo, debe especificar los valores de campo en el orden definido por la estructura de tabla.  
  
## <a name="remarks"></a>Comentarios  
 El nuevo registro contiene los datos que aparecen en la cláusula VALUES.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción INSERT de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando FoxProINSERT Visual sin traducción.  
  
## <a name="see-also"></a>Vea también  
 [Crear tabla - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Seleccione - comando SQL](../../odbc/microsoft/select-sql-command.md)
