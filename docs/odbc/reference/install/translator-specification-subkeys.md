---
title: Subclaves de especificación del traductor ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad21943c5313edcb09aba88d45ea21132aa9757f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296045"
---
# <a name="translator-specification-subkeys"></a>Subclaves de la especificación del traductor
Cada traductor que aparece en la subclave Traductores ODBC tiene una subclave propia. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave Traductores ODBC. Los valores de esta subclave enumeran las rutas completas de los archivos DLL de configuración del traductor y el traductor y el recuento de uso. Los formatos de los valores son los que se muestran en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Traductor|REG_SZ|*ruta-DLL-traductor*|  
|Configurar|REG_SZ|*setup-DLL-path*|  
|UsageCount|REG_DWORD|*count*|  
  
 Para obtener información acerca de los recuentos de uso, consulte [Recuento](../../../odbc/reference/install/usage-counting.md) de uso sin anterioridad en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este recuento.  
  
 Por ejemplo, supongamos que Microsoft Code Page Translator tiene un archivo DLL de traducción denominado Mscpxl32.dll, que las funciones de configuración del traductor están en el mismo archivo DLL y que el traductor se ha instalado tres veces. Los valores de la subclave Microsoft Code Page Translator pueden ser los siguientes:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
