---
description: 'Manipulación de datos de MDX: CALL'
title: CALL (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a8f3b550e3fed3fe28e74896c3c4ff764db8810
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387048"
---
# <a name="mdx-data-manipulation---call"></a>Manipulación de datos de MDX: CALL


  Ejecuta un procedimiento almacenado que no devuelve ningún valor en el ámbito actual u, opcionalmente, en un cubo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SP_Name*  
 Expresión de cadena válida que proporciona el nombre de un procedimiento almacenado.  
  
 *SP_Argument*  
 Expresión de cadena válida que proporciona un argumento para el procedimiento almacenado llamado.  
  
 *Cube_Expression*  
 Expresión de cubo de cadena válida que proporciona el nombre del cubo.  
  
## <a name="remarks"></a>Observaciones  
 La instrucción **Call** ejecuta un procedimiento almacenado registrado especificado, incluyendo opcionalmente uno o más argumentos para el procedimiento almacenado especificado. La instrucción **Call** solo se usa con procedimientos almacenados que devuelven valores void. Esta instrucción no puede combinarse con otras funciones u operadores en una misma expresión MDX. Los procedimientos almacenados registrados que devuelven valores pueden llamarse directamente en expresiones de MDX y combinarse con otras funciones y operadores de MDX.  
  
 Si no se especifica un cubo, la instrucción ejecuta el procedimiento almacenado en el cubo actual.  
  
> [!NOTE]  
>  Si el procedimiento almacenado no está registrado en el cliente, la instrucción **Call** intenta llamar al procedimiento almacenado desde una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de manipulación de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Using Stored Procedures &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md) (Usar procedimientos almacenados [MDX])  
  
  
