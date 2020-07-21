---
title: Quite los UDT con el nombre de los tipos de datos GEOMETRY y Geography reservados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4977d45d53e1114edc8e04ad504963bae0b9eb9d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059119"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>Quitar UDT con nombre después de los tipos de datos GEOMETRY y GEOGRAPHY reservados
  El Asesor de actualizaciones detectó un tipo definido por el usuario (UDT) que se denomina después de un término reservado para los tipos de datos `geometry` o `geography`. Los tipos de datos `geometry` y `geography` son parte de la nueva característica de datos espaciales.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Las condiciones utilizadas para los tipos de datos espaciales no se deberían utilizar como nombres para Common Language Runtime (CLR) o UDT de alias.  
  
## <a name="corrective-action"></a>Acción correctora  
 Elimine el UDT que se denomina con el tipo de datos y vuelva a crearlo con un nombre no reservado.  
  
## <a name="external-resources"></a>Recursos externos  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
