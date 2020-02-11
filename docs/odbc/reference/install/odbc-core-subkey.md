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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9380083eb5a0ad796f436af271564676b757d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094007"
---
# <a name="odbc-core-subkey"></a>Subclave de ODBC Core
El valor de la subclave ODBC Core proporciona el recuento de uso de los componentes principales (Administrador de controladores, biblioteca de cursores, DLL del instalador, etc.). El formato de este valor se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*contabiliza*|  
  
 Por ejemplo, supongamos que los programas de instalación de han instalado los componentes principales de ODBC para tres aplicaciones diferentes y dos controladores diferentes. El valor de la subclave de ODBC Core sería:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
