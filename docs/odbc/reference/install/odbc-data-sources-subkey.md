---
title: Subclave de orígenes de datos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9867946ce84163a504582c8a9575100c3c9aacd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63069824"
---
# <a name="odbc-data-sources-subkey"></a>Subclave de orígenes de datos de ODBC
Los valores bajo la subclave de orígenes de datos ODBC enumeran los orígenes de datos. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|NOMBRE|Tipo de datos|Datos|  
|----------|---------------|----------|  
|*data-source-name*|REG_SZ|*driver-description*|  
  
 El *nombre del origen de datos* valor está definido por el programa de administración (que normalmente se solicita al usuario para él), y *descripción del controlador* definido por el programador del controlador (suele ser el nombre de la DBMS asociado con el controlador).  
  
 Por ejemplo, supongamos que tres se han definido los orígenes de datos: Inventario, que usa SQL Server; Nómina, que usa dBASE; y personal, que usa archivos de texto en formato. Los valores bajo la subclave de orígenes de datos ODBC podrían ser como sigue:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
