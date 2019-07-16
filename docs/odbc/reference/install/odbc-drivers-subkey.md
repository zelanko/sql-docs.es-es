---
title: Subclave de controladores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb54ba7becad42d8d9d2c2870c02db37a3c7d89f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093981"
---
# <a name="odbc-drivers-subkey"></a>Subclave de controladores de ODBC
Los valores bajo la subclave de controladores ODBC enumeran los controladores instalados. En la tabla siguiente se muestra el formato de estos valores.  
  
|NOMBRE|Tipo de datos|Datos|  
|----------|---------------|----------|  
|*driver-description*|REG_SZ|**instalado**|  
  
 El *descripción del controlador* nombre se define mediante el programador del controlador. Suele ser el nombre del DBMS asociado al controlador.  
  
 Por ejemplo, supongamos que se han instalado los controladores para los archivos de texto con formato y SQL Server. Los valores bajo la subclave de controladores ODBC podrían ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
