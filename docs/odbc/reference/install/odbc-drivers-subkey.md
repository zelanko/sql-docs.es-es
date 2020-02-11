---
title: Subclave ODBC drivers | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093981"
---
# <a name="odbc-drivers-subkey"></a>Subclave de controladores de ODBC
Los valores de la subclave ODBC drivers enumeran los controladores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*controlador: Descripción*|REG_SZ|**Instalación**|  
  
 El nombre *de la descripción del controlador* lo define el desarrollador del controlador. Normalmente, es el nombre del DBMS asociado al controlador.  
  
 Por ejemplo, suponga que se han instalado Controladores para los archivos de texto con formato y SQL Server. Los valores de la subclave controladores ODBC pueden ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
