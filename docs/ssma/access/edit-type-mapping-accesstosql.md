---
title: "Editar la asignación de tipo (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90a03136fcc5a67382cffd99e426f8b8cfa605bd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="edit-type-mapping-accesstosql"></a>Editar la asignación de tipo (AccessToSQL)
El **Editar asignación de tipo** cuadro de diálogo permite especificar cómo se asignan los tipos entre los objetos de base de datos de origen y de destino.  
  
Puede tener acceso a este cuadro de diálogo en varios lugares:  
  
-   Cuando se selecciona una base de datos de origen o un objeto de base de datos, el **Type Mapping** ficha aparece a la derecha del explorador de metadatos. Haga clic en **agregar** para agregar una nueva asignación de tipo, o haga clic en **editar** para cambiar una asignación de tipo existente.  
  
-   En el **herramientas** menú, seleccione **configuración del proyecto** o **configuración de proyecto predeterminada**. En el cuadro de diálogo que aparece, seleccione **asignación de tipo**. Haga clic en **agregar** para agregar una nueva asignación de tipo, o haga clic en **editar** para cambiar una asignación de tipo existente.  
  
Asignaciones de tipo específico de la tabla invalidación base de datos y las asignaciones de tipos de proyecto. Las asignaciones específicas de la base de datos invalidan las asignaciones de project.  
  
## <a name="options"></a>Opciones  
**Tipo de origen**  
Seleccione el tipo de datos de origen se asignan a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos.  
  
Si el tipo de datos es de longitud variable, los siguientes campos aparecerán en **tipo de origen de**:  
  
**De**  
Especifique la longitud mínima de esta asignación. Por ejemplo, para la **texto** tipo de datos, puede especificar 10 para especificar que esta asignación es para un intervalo que comience en **Text (10)**.  
  
**Para**  
Especifique la longitud máxima de esta asignación. Por ejemplo, para la **texto** tipo de datos, puede escribir 20 para especificar que esta asignación es para un intervalo finaliza **text(20)**.  
  
**Tipo de destino**  
Seleccione el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos al que está asignado el tipo de datos de origen. Cuando SSMA crea la tabla o el procedimiento almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], cambiará el tipo de datos de origen para este tipo de datos.  
  
Si el tipo de datos es de longitud variable, el siguiente campo aparecerá bajo **tipo de destino**:  
  
**Replace with**  
Especifique la longitud de destino para esta asignación. Por ejemplo, para la **nvarchar** tipo de datos, puede escribir 20 para especificar que el tipo de datos de origen especificado debe asignarse a **nvarchar (20)**.  
  
