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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600873"
---
# <a name="odbc-data-sources-subkey"></a>Subclave de orígenes de datos de ODBC
Los valores bajo la subclave de orígenes de datos ODBC enumeran los orígenes de datos. El formato de estos valores es como se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*nombre del origen de datos*|REG_SZ|*Descripción del controlador*|  
  
 El *nombre del origen de datos* valor está definido por el programa de administración (que normalmente se solicita al usuario para él), y *descripción del controlador* definido por el programador del controlador (suele ser el nombre de la DBMS asociado con el controlador).  
  
 Por ejemplo, supongamos que se han definido tres orígenes de datos: inventario, que usa SQL Server; Nómina, que usa dBASE; y personal, que usa archivos de texto en formato. Los valores bajo la subclave de orígenes de datos ODBC podrían ser como sigue:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
