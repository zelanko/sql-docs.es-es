---
description: Subclave de controlador predeterminada
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78cc54253d002c54510fdc47f46f10de9281b65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494558"
---
# <a name="default-driver-subkey"></a>Subclave de controlador predeterminada
La subclave predeterminada contiene un valor único que describe el controlador utilizado por el origen de datos predeterminado. El formato de este valor se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|**Controlador**|REG_SZ|*default-Driver-Description*|  
  
 El nombre *predeterminado-Driver-Description* es el mismo que el nombre del valor de la subclave ODBC drivers que describe el controlador.  
  
 Por ejemplo, si el origen de datos predeterminado usa el controlador SQL Server, el valor de la subclave predeterminada podría ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  El controlador predeterminado incluido en la subclave predeterminada puede hacer referencia a un DSN de usuario predeterminado o a un DSN de sistema predeterminado. Si se han creado un DSN de usuario predeterminado y un DSN de sistema predeterminado, el controlador predeterminado viene determinado por el DSN que se creó en último lugar, por lo que es posible que no sea una entrada válida para el DSN que se creó en primer lugar.
