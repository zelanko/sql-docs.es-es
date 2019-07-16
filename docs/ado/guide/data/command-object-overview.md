---
title: Información general sobre objetos de comando | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef68a36f64fbaf72f18af9fba6f2e2781422574c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925855"
---
# <a name="command-object-overview"></a>Información general sobre objetos de comando
Con un **comando** de objeto, puede hacer lo siguiente:  
  
-   Definir el texto ejecutable del comando (por ejemplo, una instrucción SQL o un procedimiento almacenado) mediante el uso de la **CommandText** propiedad.  
  
-   Definir consultas parametrizadas o argumentos de procedimientos almacenados mediante **parámetro** objetos y el **parámetros** colección.  
  
-   Ejecutar un comando y devolver un **Recordset** objeto, si es necesario, mediante el uso de la **Execute** método.  
  
-   Especificar el tipo de comando mediante el **CommandType** propiedad antes de la ejecución para optimizar el rendimiento.  
  
-   Especificar información específica sobre el texto de comando mediante el **dialecto** propiedad de la **comando** objeto.  
  
-   Controlar si el proveedor guarda una versión preparada (o compilada) del comando antes de la ejecución mediante el uso de la **Prepared** propiedad.  
  
-   Establecer el número de segundos que esperará un proveedor para que un comando para ejecutar mediante la **CommandTimeout** propiedad.  
  
-   Asociar una conexión abierta con un **comando** objeto estableciendo sus **ActiveConnection** propiedad.  
  
-   Establecer el **nombre** propiedad para identificar el **comando** objeto como un método en el asociado **conexión** objeto.  
  
-   Pasar un **comando** de objeto para el **origen** propiedad de un **Recordset** con el fin de obtener los datos.  
  
-   Pasar un **Stream** objeto que contiene un comando (por ejemplo, un comando XML) a un proveedor que lo admite.
