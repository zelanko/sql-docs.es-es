---
title: Subclave de controladores ODBC (ODBC Drivers Subkey) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd1f8d3293e35a543cce6b5079d9c6e10a331a88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304036"
---
# <a name="odbc-drivers-subkey"></a>Subclave de controladores de ODBC
Los valores de la subclave Controladores ODBC enumeran los controladores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*descripción del conductor*|REG_SZ|**Instalado**|  
  
 El nombre *de descripción del controlador* lo define el desarrollador del controlador. Normalmente es el nombre del DBMS asociado con el controlador.  
  
 Por ejemplo, supongamos que se han instalado controladores para archivos de texto con formato y SQL Server. Los valores de la subclave Controladores ODBC pueden ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
