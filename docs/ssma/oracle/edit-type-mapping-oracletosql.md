---
title: "Editar la asignación de tipo (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: b737d23608fa538019d55cc4825a29001238ee1e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="edit-type-mapping-oracletosql"></a>Editar la asignación de tipo (OracleToSQL)
El **Editar asignación de tipo** cuadro de diálogo permite especificar cómo se asignan los tipos entre los objetos de base de datos de origen y de destino.  
  
Puede tener acceso a este cuadro de diálogo en varios lugares:  
  
-   Cuando se selecciona una base de datos de origen o un objeto de base de datos, el **Type Mapping** ficha aparece a la derecha del explorador de metadatos. Haga clic en **agregar** para agregar una nueva asignación de tipo, o haga clic en **editar** para cambiar una asignación de tipo existente.  
  
-   En el **herramientas** menú, seleccione **configuración del proyecto** o **configuración de proyecto predeterminada**. En el cuadro de diálogo que aparece, seleccione **asignación de tipo**. Haga clic en **agregar** para agregar una nueva asignación de tipo, o haga clic en **editar** para cambiar una asignación de tipo existente.  
  
Asignaciones de tipo específico de la tabla invalidación base de datos y las asignaciones de tipos de proyecto. Las asignaciones específicas de la base de datos invalidan las asignaciones de project.  
  
## <a name="options"></a>.  
**Tipo de origen**  
Seleccione el tipo de datos de origen se asignan a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos.  
  
Si el tipo de datos es de longitud variable, los siguientes campos aparecerán en **tipo de origen de**:  
  
**De**  
Especifique la longitud mínima de esta asignación. Por ejemplo, para la **nchar** tipo de datos, puede especificar 10 para especificar que esta asignación es para un intervalo que comience en **nchar(10)**.  
  
**Para**  
Especifique la longitud máxima de esta asignación. Por ejemplo, para la **nchar** tipo de datos, puede escribir 20 para especificar que esta asignación es para un intervalo finaliza **nchar (20)**.  
  
**Tipo de destino**  
Seleccione el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos al que está asignado el tipo de datos de origen. Cuando SSMA crea la tabla o el procedimiento almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], cambiará el tipo de datos de origen para este tipo de datos.  
  
Si el tipo de datos es de longitud variable, el siguiente campo aparecerá bajo **tipo de destino**:  
  
**Replace with**  
Especifique la longitud de destino para esta asignación. Por ejemplo, para la **nvarchar** tipo de datos, puede escribir 20 para especificar que el tipo de datos de origen especificado debe asignarse a **nvarchar (20)**.  
  
