---
title: Subclaves de especificación de traductor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec94f3e02b720617e8f7369b12a916c2bbbe7b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093800"
---
# <a name="translator-specification-subkeys"></a>Subclaves de la especificación del traductor
Cada Traductor enumerado en la subclave traductores ODBC tiene una subclave propia. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave traductores ODBC. Los valores de esta subclave muestran las rutas de acceso completas de los archivos dll de configuración de traductor y traductor y el recuento de uso. Los formatos de los valores son los que se muestran en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|Traductor|REG_SZ|*Translator-DLL-ruta de acceso*|  
|Instalación|REG_SZ|*Setup-DLL-path*|  
|UsageCount|REG_DWORD|*contabiliza*|  
  
 Para obtener información acerca de los recuentos de uso, consulte [recuento de uso](../../../odbc/reference/install/usage-counting.md) anteriormente en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este recuento.  
  
 Por ejemplo, supongamos que el traductor de páginas de códigos de Microsoft tiene un archivo DLL de traducción denominado Mscpxl32. dll, que las funciones de configuración del traductor están en el mismo archivo DLL y que el traductor se ha instalado tres veces. Los valores de la subclave traductor de página de códigos de Microsoft podrían ser los siguientes:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
