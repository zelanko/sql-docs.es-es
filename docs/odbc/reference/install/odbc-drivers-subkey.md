---
title: Subclave de controladores ODBC | Documentos de Microsoft
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
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 756f1f145d7e9a8ea5698366af920cce13041dd2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-drivers-subkey"></a>Subclave de controladores ODBC
Los valores bajo la subclave de controladores ODBC enumeran los controladores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*Descripción del controlador*|REG_SZ|**Instalado**|  
  
 El *descripción del controlador* nombre viene definido por el programador del controlador. Normalmente es el nombre del DBMS asociado al controlador.  
  
 Por ejemplo, suponga que se instalaron los controladores para los archivos de texto con formato y SQL Server. Los valores bajo la subclave de controladores ODBC pueden ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
