---
title: Subclave de controlador por defecto ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb134d670964e352d94c13474d8a72fa4bd494ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301058"
---
# <a name="default-driver-subkey"></a>Subclave de controlador predeterminada
La subclave Default contiene un único valor que describe el controlador utilizado por el origen de datos predeterminado. El formato de este valor se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|**Controlador**|REG_SZ|*default-driver-description*|  
  
 El nombre *default-driver-description* es el mismo que el nombre del valor en la subclave Controladores ODBC que describe el controlador.  
  
 Por ejemplo, si el origen de datos predeterminado utiliza el controlador de SQL Server, el valor de la subclave Predeterminado podría ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  El controlador predeterminado contenido en la subclave Predeterminado puede hacer referencia a un DSN de usuario predeterminado o a un DSN de sistema predeterminado. Si se han creado un DSN de usuario predeterminado y un DSN de sistema predeterminado, el controlador predeterminado viene determinado por el DSN que se creó en último lugar, por lo que podría no ser una entrada válida para el DSN que se creó primero.
