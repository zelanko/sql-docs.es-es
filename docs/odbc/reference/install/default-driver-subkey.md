---
title: Subclave de controlador predeterminada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d78101fd564e18467e6833f480cec2409dc2c44b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198309"
---
# <a name="default-driver-subkey"></a>Subclave de controlador predeterminada
La subclave predeterminada contiene un valor único que describe el controlador utilizado por el origen de datos de forma predeterminada. El formato de este valor se muestra en la tabla siguiente.  
  
|Name|Tipo de datos|Datos|  
|----------|---------------|----------|  
|**Controlador**|REG_SZ|*default-driver-description*|  
  
 El *descripción del controlador predeterminado* nombre es el mismo que el nombre del valor bajo la subclave de controladores ODBC que describe el controlador.  
  
 Por ejemplo, si el origen de datos de forma predeterminada, usa el controlador de SQL Server, el valor bajo la subclave predeterminada podría ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  El controlador predeterminado de contenidos en la subclave predeterminada puede hacer referencia a un DSN de usuario predeterminado o un DSN de sistema de forma predeterminada. Si un DSN de usuario predeterminado y un sistema predeterminado DSN se han creado, el controlador predeterminado viene determinada por el DSN que se creó por última vez, por lo que quizás no sea una entrada válida para el DSN que creó en primer lugar.
