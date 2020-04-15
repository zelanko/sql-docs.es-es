---
title: Subclave de núcleo ODBC (ODBC Core Subkey) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304065"
---
# <a name="odbc-core-subkey"></a>Subclave de ODBC Core
El valor de la subclave ODBC Core proporciona el recuento de uso de los componentes principales (Administrador de controladores, biblioteca de cursores, DLL del instalador, etc.). El formato de este valor se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 Por ejemplo, supongamos que los programas de instalación han instalado los componentes ODBC Core para tres aplicaciones diferentes y dos controladores diferentes. El valor bajo la subclave ODBC Core sería:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
