---
title: "Las subclaves de la especificación del origen de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61b485f55be504e894754f74c4ab779b9ebbaf5a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-specification-subkeys"></a>Subclaves de especificación del origen de datos
Cada origen de datos aparece en la subclave de orígenes de datos ODBC tiene una subclave de su propio. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave de orígenes de datos ODBC. Los valores bajo esta subclave deben la DLL del controlador en la lista y pueden mostrar una descripción del origen de datos. Si el controlador admite traductores, los valores pueden enumerar el nombre de un traductor de manera predeterminada, el archivo DLL de traducción predeterminado y la opción de traducción predeterminado. Los valores también pueden mostrar otra información requerida por el controlador para conectarse al origen de datos. Por ejemplo, el controlador podría requerir un nombre de servidor, el nombre de base de datos o el nombre del esquema.  
  
 Los formatos de los valores son como se muestra en la tabla siguiente. Solo el valor de controlador es obligatorio.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*Descripción*|  
|Controlador|REG_SZ|*ruta de DLL*|  
|TranslationDLL|REG_SZ|*ruta de la DLL de traductor*|  
|TranslationName|REG_SZ|*nombre de traductor*|  
|TranslationOption|REG_SZ|*opción de traducción*|  
|*nombre del valor participar*|*tipo de valor participar*|*datos del valor participar*|  
  
 Por ejemplo, suponga que el controlador de SQL Server requiere el nombre del servidor y una marca para OEM a la conversión de ANSI y define los valores de servidor y OEMTOANSI para estos. Suponga también que el origen de datos de inventario utiliza el traductor de páginas de código de Microsoft® para traducir entre los Windows® Latín 1 (1250) y páginas de códigos multilingüe (850). Los valores bajo la subclave de inventario podrían ser el siguiente:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```

