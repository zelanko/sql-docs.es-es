---
title: Editar asignación de tipo (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 513f071a-d5e6-4ed5-acca-269bf76323c5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d6daf0e74ff8c7a7c65441bc98afc9c47964ef0b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633030"
---
# <a name="edit-type-mapping-sybasetosql"></a>Editar asignación de tipo (SybaseToSQL)
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
Especificar la longitud mínima para esta asignación. Por ejemplo, para el **nchar** tipo de datos, puede escribir 10 para especificar que esta asignación es para un intervalo que comienza en **nchar(10)**.  
  
**Para**  
Especifique la longitud máxima de esta asignación. Por ejemplo, para el **nchar** tipo de datos, puede escribir 20 para especificar que esta asignación es para un intervalo finaliza en **nchar (20)**.  
  
**Tipo de destino**  
Seleccione el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos al que está asignado el tipo de datos de origen. Cuando SSMA crea la tabla o procedimiento almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cambiará el tipo de datos de origen para este tipo de datos.  
  
Si el tipo de datos es de longitud variable, el siguiente campo aparecerá bajo **tipo de destino**:  
  
**Replace with**  
Especifique la longitud de destino para esta asignación. Por ejemplo, para el **nvarchar** tipo de datos, puede escribir 20 para especificar que el tipo de datos de origen especificado debe asignarse a **nvarchar (20)**.  
  
