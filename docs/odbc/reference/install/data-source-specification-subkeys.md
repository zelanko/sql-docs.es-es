---
description: Subclaves de la especificación del origen de datos
title: Subclaves de especificación de origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fabfd07779f74945bf647d20075de0cc057710b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494570"
---
# <a name="data-source-specification-subkeys"></a>Subclaves de la especificación del origen de datos
Cada origen de datos que aparece en la subclave de orígenes de datos ODBC tiene una subclave propia. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave de orígenes de datos ODBC. Los valores de esta subclave deben mostrar la DLL del controlador y pueden mostrar una descripción del origen de datos. Si el controlador admite traductores, los valores pueden enumerar el nombre de un traductor predeterminado, el archivo DLL de traducción predeterminado y la opción de traducción predeterminada. Los valores también pueden mostrar otra información necesaria para que el controlador se conecte al origen de datos. Por ejemplo, el controlador podría requerir un nombre de servidor, un nombre de base de datos o un nombre de esquema.  
  
 Los formatos de los valores son los que se muestran en la tabla siguiente. Solo se requiere el valor del controlador.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Descripción|REG_SZ|*description*|  
|Controlador|REG_SZ|*Driver-DLL-path*|  
|TranslationDLL|REG_SZ|*Translator-DLL-ruta de acceso*|  
|TranslationName|REG_SZ|*nombre del traductor*|  
|TranslationOption|REG_SZ|*Translation-opción*|  
|*nombre del valor opt*|*tipo de valor opt*|*datos de valor opt*|  
  
 Por ejemplo, supongamos que el controlador de SQL Server requiere el nombre del servidor y una marca para la conversión de OEM a ANSI y define los valores Server y OEMTOANSI para ellos. Supongamos también que el origen de datos de inventario utiliza el traductor de páginas de códigos de Microsoft® para traducir entre las páginas de códigos de Windows® Latin 1 (1250) y multilingüe (850). Los valores de la subclave Inventory pueden ser los siguientes:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
