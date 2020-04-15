---
title: Subclaves de especificación de origen de datos ? Microsoft Docs
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
ms.openlocfilehash: 281377c307f3f3750e87bf5dc988beb7660067af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300345"
---
# <a name="data-source-specification-subkeys"></a>Subclaves de la especificación del origen de datos
Cada origen de datos enumerado en la subclave Orígenes de datos ODBC tiene una subclave propia. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave Orígenes de datos ODBC. Los valores de esta subclave deben enumerar el archivo DLL del controlador y pueden enumerar una descripción del origen de datos. Si el controlador admite traductores, los valores pueden enumerar el nombre de un traductor predeterminado, el archivo DLL de traducción predeterminado y la opción de traducción predeterminada. Los valores también pueden enumerar otra información requerida por el controlador para conectarse al origen de datos. Por ejemplo, el controlador puede requerir un nombre de servidor, un nombre de base de datos o un nombre de esquema.  
  
 Los formatos de los valores son los que se muestran en la tabla siguiente. Solo se requiere el valor Driver.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Descripción|REG_SZ|*Descripción*|  
|Controlador|REG_SZ|*driver-DLL-path*|  
|TranslationDLL|REG_SZ|*ruta-DLL-traductor*|  
|TranslationName|REG_SZ|*nombre-traductor*|  
|TranslationOption|REG_SZ|*traducción-opción*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 Por ejemplo, supongamos que el controlador de SQL Server requiere el nombre del servidor y una marca para la conversión de OEM a ANSI y define los valores server y OEMTOANSI para estos. Supongamos también que el origen de datos Inventory utiliza Microsoft® Editor de páginas de códigos para traducir entre las páginas de códigos de Windows® Latin 1 (1250) y Multilingual (850). Los valores de la subclave Inventario pueden ser los siguientes:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
