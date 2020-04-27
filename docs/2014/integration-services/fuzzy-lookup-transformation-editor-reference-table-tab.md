---
title: Editor de transformación búsqueda aproximada (pestaña tabla de referencia) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c9fb11308ae60cf061f184ade467d814d6a10fc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058306"
---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>Editor de transformación Búsqueda aproximada (pestaña Tabla de referencia)
  Use la pestaña **Tabla de referencia** del cuadro de diálogo **Editor de transformación Búsqueda aproximada** para especificar la tabla de origen y el índice que se van a usar para la búsqueda. El origen de los datos de referencia debe ser una tabla de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  La transformación Búsqueda aproximada crea una copia de trabajo de la tabla de referencia. Los índices descritos a continuación se crean en esta tabla de trabajo mediante una tabla especial, no un índice normal de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La transformación no modifica las tablas de origen existentes a menos que se seleccione **Mantener el índice almacenado**. En este caso, se crea un desencadenador en la tabla de referencia que actualiza la tabla de trabajo y la tabla del índice de búsqueda basándose en los cambios en la tabla de referencia.  
  
> [!NOTE]  
>  Las `Exhaustive` `MaxMemoryUsage` propiedades y de la transformación búsqueda aproximada no están disponibles en el **Editor de transformación búsqueda aproximada**, pero se pueden establecer mediante el **editor avanzado**. Además, solo se puede especificar un valor mayor `MaxOutputMatchesPerInput` que 100 para en el **editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre la transformación Búsqueda aproximada en [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para obtener más información acerca de la transformación Búsqueda aproximada, vea [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones de OLE DB**  
 Seleccione un administrador de conexiones OLE DB de la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nuevo**  
 Cree una conexión mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Generar índice nuevo**  
 Especifique que la transformación debe crear un nuevo índice que se utilizará en la búsqueda.  
  
 **Nombre de la tabla de referencia**  
 Seleccione la tabla existente que se utilizará como tabla de referencia (búsqueda).  
  
 **Almacenar el nuevo índice**  
 Seleccione esta opción si desea guardar el nuevo índice de búsqueda.  
  
 **Nombre del índice nuevo**  
 Si ha elegido guardar el índice de búsqueda nuevo, escriba un nombre descriptivo para el índice.  
  
 **Mantener el índice almacenado**  
 Si ha elegido guardar el índice de búsqueda nuevo, especifique si también desea que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mantenga el índice.  
  
> [!NOTE]  
>  Al seleccionar **Mantener el índice almacenado** en la pestaña **Tabla de referencia** del **Editor de transformación Búsqueda aproximada**, la transformación utiliza los procedimientos almacenados administrados para mantener el índice. Estos procedimientos almacenados administrados usan la característica de integración de Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. De forma predeterminada, la integración de CLR en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no está habilitada. Para utilizar la funcionalidad **Mantener el índice almacenado** , debe habilitar la integración de CLR. Para más información, consulte [Enabling CLR Integration](../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Dado que la opción **Mantener el índice almacenado** requiere la integración con CLR, esta característica solo funciona al seleccionar una tabla de referencia en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] donde se habilite la integración con CLR.  
  
 **Usar índice existente**  
 Especifique que la transformación debe utilizar un índice existente para la búsqueda.  
  
 **Nombre de un índice existente**  
 Seleccione de la lista un índice de búsqueda creado previamente.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación búsqueda aproximada &#40;pestaña columnas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor de transformación Búsqueda aproximada &#40;pestaña Avanzadas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
