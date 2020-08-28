---
description: Información general sobre objetos de comando
title: Información general sobre el objeto Command | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: rothja
ms.author: jroth
ms.openlocfilehash: e0f1616fa83f1fed5a22de6fc1a1ee443bdddd82
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991566"
---
# <a name="command-object-overview"></a>Información general sobre objetos de comando
Con un objeto de **comando** , puede hacer lo siguiente:  
  
-   Defina el texto ejecutable del comando (por ejemplo, una instrucción SQL o un procedimiento almacenado) mediante la propiedad **CommandText** .  
  
-   Defina consultas con parámetros o argumentos de procedimientos almacenados mediante el uso de objetos de **parámetro** y la colección de **parámetros** .  
  
-   Ejecutar un comando y devolver un objeto de **conjunto de registros** , si es necesario, mediante el método **Execute** .  
  
-   Especifique el tipo de comando mediante la propiedad **CommandType** antes de la ejecución para optimizar el rendimiento.  
  
-   Especifique información específica sobre el texto del comando mediante la propiedad **Dialect** del objeto **Command** .  
  
-   Controlar si el proveedor guarda una versión preparada (o compilada) del comando antes de la ejecución mediante la propiedad **Prepared** .  
  
-   Establezca el número de segundos que un proveedor esperará a que se ejecute un comando mediante la propiedad **CommandTimeout** .  
  
-   Asocie una conexión abierta a un objeto de **comando** estableciendo su propiedad **ActiveConnection** .  
  
-   Establezca la propiedad **nombre** para identificar el objeto de **comando** como un método en el objeto de **conexión** asociado.  
  
-   Pase un objeto de **comando** a la propiedad de **origen** de un **conjunto de registros** para obtener los datos.  
  
-   Pase un objeto de **flujo** que contenga un comando (por ejemplo, un comando XML) a un proveedor que lo admita.
