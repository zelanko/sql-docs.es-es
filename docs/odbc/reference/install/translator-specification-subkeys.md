---
title: Subclaves de la especificación de traductor | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093800"
---
# <a name="translator-specification-subkeys"></a>Subclaves de la especificación del traductor
Traductor enumerado en la subclave de traductores de ODBC tiene una subclave de su propio. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave de traductores de ODBC. Los valores bajo esta subclave enumeran las rutas de acceso completas de traductor y las DLL de instalación de traductor y el recuento de uso. Los formatos de los valores son como se muestra en la tabla siguiente.  
  
|Name|Tipo de datos|Datos|  
|----------|---------------|----------|  
|Traductor|REG_SZ|*translator-DLL-path*|  
|Programa de instalación|REG_SZ|*setup-DLL-path*|  
|UsageCount|REG_DWORD|*Recuento*|  
  
 Para obtener información sobre recuentos de uso, consulte [recuento de uso](../../../odbc/reference/install/usage-counting.md) anteriormente en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este número.  
  
 Por ejemplo, supongamos que la página de código de Microsoft Translator tiene una archivo DLL denominado Mscpxl32.dll, que las funciones de traductor el programa de instalación están en el mismo archivo DLL de traducción y que se ha instalado el traductor de tres veces. Los valores bajo la subclave de la página de código de Microsoft Translator podrían ser como sigue:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
