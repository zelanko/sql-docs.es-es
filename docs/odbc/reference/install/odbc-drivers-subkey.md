---
description: Subclave de controladores de ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b950a352c3da69a2a8de9a89f7bbebf87e0a597a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448925"
---
# <a name="odbc-drivers-subkey"></a>Subclave de controladores de ODBC
Los valores de la subclave ODBC drivers enumeran los controladores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*controlador: Descripción*|REG_SZ|**Instalado**|  
  
 El nombre *de la descripción del controlador* lo define el desarrollador del controlador. Normalmente, es el nombre del DBMS asociado al controlador.  
  
 Por ejemplo, suponga que se han instalado Controladores para los archivos de texto con formato y SQL Server. Los valores de la subclave controladores ODBC pueden ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
