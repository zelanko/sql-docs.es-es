---
title: "Información general sobre objetos de comando | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 175c3793a41c4502a0c558c63e4eec89b35cd02f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="command-object-overview"></a>Información general sobre objetos de comando
Con un **comando** de objeto, puede hacer lo siguiente:  
  
-   Definir el texto ejecutable del comando (por ejemplo, una instrucción SQL o un procedimiento almacenado) mediante la **CommandText** propiedad.  
  
-   Definir consultas parametrizadas o argumentos de procedimientos almacenados mediante **parámetro** objetos y **parámetros** colección.  
  
-   Ejecutar un comando y devolver un **Recordset** objeto, si es necesario, mediante el uso de la **Execute** método.  
  
-   Especificar el tipo de comando mediante el **CommandType** propiedad antes de la ejecución para optimizar el rendimiento.  
  
-   Especificar información específica sobre el texto de comando mediante el **dialecto** propiedad de la **comando** objeto.  
  
-   Controlar si el proveedor guarda una versión preparada (o compilada) del comando antes de la ejecución mediante el uso de la **Prepared** propiedad.  
  
-   Establecer el número de segundos que esperará un proveedor para que un comando para ejecutar mediante el uso de la **CommandTimeout** propiedad.  
  
-   Asociar una conexión abierta con un **comando** objeto estableciendo su **ActiveConnection** propiedad.  
  
-   Establecer el **nombre** propiedad para identificar el **comando** objeto como un método en el asociado **conexión** objeto.  
  
-   Pasar un **comando** el objeto a la **origen** propiedad de un **Recordset** con el fin de obtener los datos.  
  
-   Pasar un **flujo** objeto que contiene un comando (por ejemplo, un comando XML) a un proveedor que admita esa situación.
