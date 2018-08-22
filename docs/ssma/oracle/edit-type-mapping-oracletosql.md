---
title: Editar asignación de tipo (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: c9225773588810e4843525e271faa7023d9ce172
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394709"
---
# <a name="edit-type-mapping-oracletosql"></a>Editar asignación de tipo (OracleToSQL)
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
  
