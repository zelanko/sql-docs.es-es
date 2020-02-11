---
title: Crear conjuntos con nombre de ámbito de sesión (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- CREATE SET statement
- session-scoped named sets [MDX]
ms.assetid: b751e1e4-6d4c-4d36-a28d-ffdaaee0f1c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 545bbdb171388f06c28644e0b8caa48db95e7e7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074044"
---
# <a name="creating-session-scoped-named-sets-mdx"></a>Crear conjuntos con nombre de ámbito de sesión (MDX)
  Para crear un conjunto con nombre que esté disponible en una sesión de expresiones multidimensionales (MDX), se usa la instrucción [CREATE SET](/sql/mdx/mdx-data-definition-create-set). Un conjunto con nombre creado mediante la instrucción CREATE SET no se quitará hasta que se cierre la sesión MDX.  
  
 Como se indica en este tema, la sintaxis de la palabra clave WITH es muy simple y fácil de usar.  
  
> [!NOTE]  
>  Para obtener más información sobre los conjuntos con nombre, vea [Crear conjuntos con nombre en MDX &#40;MDX&#41;](mdx-named-sets-building-named-sets.md).  
  
## <a name="create-set-syntax"></a>Sintaxis de CREATE SET  
 Utilice la siguiente sintaxis para la instrucción CREATE SET:  
  
```  
CREATE SESSION SET [CURRENTCUBE. | <cube name>.]<Set Identifier> AS <Set Expression>  
```  
  
 En la sintaxis de CREATE SET, el parámetro `cube name` contiene el nombre del cubo que incluye los miembros del conjunto con nombre. Si no se especifica el parámetro `cube name` , se utilizará el cubo actual como el cubo que contiene el miembro del conjunto con nombre. Por otra parte, el parámetro `Set_Identifier` incluye el alias del conjunto con nombre; el parámetro `Set_Expression` , por su parte, contiene la expresión de conjunto a la que hará referencia el alias del conjunto con nombre.  
  
## <a name="create-set-example"></a>Ejemplo de CREATE SET  
 En el siguiente ejemplo se utiliza la instrucción CREATE SET para crear el conjunto con nombre `SetCities_2_3` basado en el cubo Store. Los miembros del conjunto con nombre `SetCities_2_3` son los almacenes de City 2 y City 3.  
  
```  
create Session set [Store].[SetCities_2_3] as  
{[Data Stores].[ByLocation].[State].&[CA].&[City 02],  
[Data Stores].[ByLocation].[State].&[NH].&[City 03]}  
```  
  
 El uso de la instrucción CREATE SET para definir el conjunto con nombre `SetCities_2_3` hace que este conjunto con nombre permanezca disponible mientras esté activa la sesión MDX actual. El siguiente ejemplo es una consulta válida que devuelve los miembros City 2 y City 3 y que puede ejecutarse en cualquier momento una vez creado el conjunto con nombre `SetCities_2_3` y antes de que se cierre la sesión.  
  
```  
select SetCities_2_3 on 0 from [Store]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Crear conjuntos con nombre de ámbito de consulta &#40;&#41;MDX](mdx-named-sets-creating-query-scoped-named-sets.md)  
  
  
