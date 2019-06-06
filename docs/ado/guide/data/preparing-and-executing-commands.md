---
title: Preparar y ejecutar comandos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6bf2120468a00de2150f6105f4d79ec5a2ed4278
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700459"
---
# <a name="preparing-and-executing-commands"></a>Preparar y ejecutar comandos
Los comandos son instrucciones emitidas a un proveedor para realizar algunas operaciones en el origen de datos subyacente. Una instrucción SQL, por ejemplo, es un comando para el proveedor de datos SQL de Microsoft. En ADO, los comandos se suelen representar por **comando** objetos, aunque también se pueden emitir comandos sencillos a través de **conexión** o **Recordset** objetos.  
  
 Puede usar el **comando** objeto para solicitar cualquier tipo compatible de operación del proveedor, suponiendo que el proveedor pueda interpretar correctamente la cadena de comandos. Es una operación común para los proveedores de datos consultar una base de datos y devolver los registros en un **Recordset** objeto que puede considerarse como un contenedor para almacenar el resultado y una herramienta para ver el resultado. Al igual que con muchos objetos ADO, algunos **comando** colecciones de objetos, métodos o propiedades podrían generar errores cuando se hace referencia a, dependiendo de la funcionalidad del proveedor.  
  
 Además de usar **comando** objetos, puede utilizar el **Execute** método en el **conexión** objeto o la **abierto** método en el  **Conjunto de registros** objeto para emitir un comando y que se ejecute. Sin embargo, debe usar un **comando** objeto si tiene que volver a usar un comando en el código, o si necesita pasar información detallada de los parámetros con el comando. Estos escenarios se tratan con más detalle más adelante en esta sección.  
  
> [!NOTE]
>  Ciertos **comando**s puede devolver un conjunto de resultados como una secuencia binaria o como una sola **registro** en lugar de como un **Recordset**, si esto es compatible con el proveedor. Además, algunos **comando**s no están pensadas para que se devuelve ningún resultado que se establece en absoluto (por ejemplo, una consulta Update de SQL). Esta sección explica el escenario más típico, sin embargo: ejecutar **comando**que devuelven resultados como un **Recordset** objeto. Para obtener más información sobre cómo devolver los resultados en **registro**s o **Stream**s, consulte [registros y secuencias](../../../ado/guide/data/records-and-streams.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Información general sobre objetos de comando](../../../ado/guide/data/command-object-overview.md)  
  
-   [Crear y ejecutar un comando Simple](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Parámetros del objeto Command](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Llamar a un procedimiento almacenado con un comando](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Llamar a un procedimiento almacenado como un método en un objeto de conexión](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Comandos con nombre](../../../ado/guide/data/named-commands.md)  
  
-   [Pasar parámetros a un comando con nombre](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
