---
title: Editar la asignación de tipos (AccessToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006575"
---
# <a name="edit-type-mapping-accesstosql"></a>Editar la asignación de tipos (AccessToSQL)
El cuadro de diálogo **Editar asignación de tipos** permite especificar cómo se asignan los tipos entre los objetos de base de datos de origen y de destino.  
  
Puede tener acceso a este cuadro de diálogo en varios lugares:  
  
-   Al seleccionar una base de datos de origen o un objeto de base de datos, la pestaña **asignación de tipos** aparece a la derecha del explorador de metadatos. Haga clic en **Agregar** para agregar una nueva asignación de tipos o haga clic en **Editar** para cambiar una asignación de tipos existente.  
  
-   En el menú **herramientas** , seleccione **configuración del proyecto** o **configuración predeterminada del proyecto**. En el cuadro de diálogo resultante, seleccione **asignación de tipos**. Haga clic en **Agregar** para agregar una nueva asignación de tipos o haga clic en **Editar** para cambiar una asignación de tipos existente.  
  
Las asignaciones de tipos específicas de tabla invalidan las asignaciones de tipo de proyecto y base de datos. Las asignaciones específicas de la base de datos invalidan las asignaciones del proyecto.  
  
## <a name="options"></a>Opciones  
**Tipo de origen**  
Seleccione el tipo de datos de origen que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] va a asignar a un tipo de datos.  
  
Si el tipo de datos es de longitud variable, los campos siguientes aparecerán en **tipo de origen**:  
  
**De**  
Especifique la longitud mínima de esta asignación. Por ejemplo, para el tipo de datos de **texto** , puede especificar 10 para especificar que esta asignación es para un intervalo que comienza en el **texto (10)**.  
  
**Para**  
Especifique la longitud máxima de esta asignación. Por ejemplo, para el tipo de datos de **texto** , puede especificar 20 para especificar que esta asignación es para un intervalo que termina en el **texto (20)**.  
  
**Tipo de destino**  
Seleccione el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos al que se asigna el tipo de datos de origen. Cuando SSMA crea la tabla o el procedimiento almacenado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en, el tipo de datos de origen cambiará a este tipo de datos.  
  
Si el tipo de datos es de longitud variable, el siguiente campo aparecerá en **tipo de destino**:  
  
**Reemplazar por**  
Especifique la longitud de destino de esta asignación. Por ejemplo, para el tipo de datos **nvarchar** , puede especificar 20 para especificar que el tipo de datos de origen especificado debe estar asignado a **nvarchar (20)**.  
  
