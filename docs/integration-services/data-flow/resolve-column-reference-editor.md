---
description: Resolver el editor de referencias de columna
title: Resolver el editor de referencias de columna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3610ee6cd8a2033a67c23051ca3bd47952ac318f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484548"
---
# <a name="resolve-column-reference-editor"></a>Resolver el editor de referencias de columna

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Cuando una ruta de acceso de entrada está desconectada o si hay columnas no asignadas en la ruta de acceso, se muestra un icono de error al lado de la ruta de acceso de datos correspondiente. Para simplificar la resolución de los errores de referencia de columna, el editor de resolución de referencias permite vincular las columnas de salida no asignadas con las columnas de entrada no asignadas para todas las rutas de acceso en el árbol de ejecución. El editor de resolución de referencias también resaltará las rutas de acceso para indicar cuáles de ellas se están resolviendo.  
  
> [!NOTE]  
>  Es posible editar un componente aunque su ruta de acceso de entrada esté desconectada.  
  
 Una vez resueltas todas las referencias de columna, si no hay otros errores de ruta de acceso de datos, no se mostrarán iconos de error al lado de las rutas de acceso de datos.  
  
## <a name="options"></a>Opciones  
 **Columnas de salida no asignadas (origen)**     
 Columnas de la ruta de acceso de nivel superior que no están asignadas actualmente.  
  
**Columnas asignadas (origen)**     
 Columnas de la ruta de acceso de nivel superior que están asignadas a columnas de la ruta de acceso de nivel inferior.  
  
**Columnas asignadas (destino)**     
 Columnas de la ruta de acceso de nivel superior que están asignadas a columnas de la ruta de acceso de nivel inferior.  
  
**Columnas de entrada no asignadas (destino)**     
 Columnas de la ruta de acceso de nivel inferior que no están asignadas actualmente.  
  
**Eliminar columnas de entrada no asignadas**  
 Active Eliminar columnas de entrada no asignadas para omitir las columnas no asignadas en el destino de la ruta de acceso de datos. El botón Vista previa de los cambios muestra una lista de los cambios que se producirán cuando presione el botón Aceptar.  
  
  
