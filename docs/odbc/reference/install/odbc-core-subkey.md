---
title: Subclave de ODBC Core | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9e6bfcf3c1efa87076e6d3e27a438cde6f794157
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304065"
---
# <a name="odbc-core-subkey"></a>Subclave de ODBC Core
El valor de la subclave ODBC Core proporciona el recuento de uso de los componentes principales (Administrador de controladores, biblioteca de cursores, DLL del instalador, etc.). El formato de este valor se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 Por ejemplo, supongamos que los programas de instalación de han instalado los componentes principales de ODBC para tres aplicaciones diferentes y dos controladores diferentes. El valor de la subclave de ODBC Core sería:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
