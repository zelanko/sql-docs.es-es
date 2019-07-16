---
title: Editar asignación de tipo (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7d41fc2f01e2cfbc2b20c58ea9be640f2afd8ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006575"
---
# <a name="edit-type-mapping-accesstosql"></a>Editar asignación de tipo (AccessToSQL)
El **Editar asignación de tipo** cuadro de diálogo le permite especificar cómo se asignan los tipos entre los objetos de base de datos de origen y destino.  
  
Puede tener acceso a este cuadro de diálogo en varios lugares:  
  
-   Cuando se selecciona una base de datos de origen o un objeto de base de datos, el **Type Mapping** ficha aparece a la derecha del explorador de metadatos. Haga clic en **agregar** para agregar una nueva asignación de tipo, o haga clic en **editar** para cambiar una asignación de tipo existente.  
  
-   En el **herramientas** menú, seleccione **configuración del proyecto** o **configuración de proyecto predeterminada**. En el cuadro de diálogo resultante, seleccione **Type Mapping**. Haga clic en **agregar** para agregar una nueva asignación de tipo, o haga clic en **editar** para cambiar una asignación de tipo existente.  
  
Asignaciones de tipos específicos de la tabla invalidación base de datos y las asignaciones de tipos de proyecto. Asignaciones específicas de la base de datos invalidan las asignaciones de project.  
  
## <a name="options"></a>Opciones  
**Tipo de origen**  
Seleccione el tipo de datos de origen para asignar a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.  
  
Si el tipo de datos es de longitud variable, los siguientes campos aparecerán en **tipo de origen**:  
  
**De**  
Especificar la longitud mínima para esta asignación. Por ejemplo, para el **texto** tipo de datos, puede escribir 10 para especificar que esta asignación es para un intervalo que comienza en **Text (10)** .  
  
**Para**  
Especifique la longitud máxima de esta asignación. Por ejemplo, para el **texto** tipo de datos, puede escribir 20 para especificar que esta asignación es para un intervalo finaliza en **text(20)** .  
  
**Tipo de destino**  
Seleccione el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos al que está asignado el tipo de datos de origen. Cuando SSMA crea la tabla o procedimiento almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cambiará el tipo de datos de origen para este tipo de datos.  
  
Si el tipo de datos es de longitud variable, el siguiente campo aparecerá bajo **tipo de destino**:  
  
**Replace with**  
Especifique la longitud de destino para esta asignación. Por ejemplo, para el **nvarchar** tipo de datos, puede escribir 20 para especificar que el tipo de datos de origen especificado debe asignarse a **nvarchar (20)** .  
  
