---
title: "Orígenes de datos ODBC subclave | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3d2ed7d39772237f522320f227c49c773d12801
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-data-sources-subkey"></a>Subclave de orígenes de datos ODBC
Los valores bajo la subclave de orígenes de datos ODBC enumeran los orígenes de datos. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*nombre del origen de datos*|REG_SZ|*Descripción del controlador*|  
  
 El *nombre de origen de datos* valor está definido por el programa de administración (que normalmente se pide al usuario para él), y *descripción del controlador* definido por el programador del controlador (suele ser el nombre de la DBMS asociado con el controlador).  
  
 Por ejemplo, suponga que se han definido tres orígenes de datos: inventario, que usa SQL Server; Nómina, que utiliza dBASE; y personal, archivos de texto de formato que utiliza. Los valores bajo la subclave de orígenes de datos ODBC podrían ser el siguiente:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
