---
description: 'Definición de datos de MDX: REFRESH CUBE'
title: REFRESH CUBE (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05ae95c97ae21d3b8ff7b4e457cf3ddf8cc38989
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387059"
---
# <a name="mdx-data-definition---refresh-cube"></a>Definición de datos de MDX: REFRESH CUBE


  Actualiza la caché de cliente para un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona un nombre de cubo.  
  
## <a name="remarks"></a>Observaciones  
 En el caso de las aplicaciones cliente conectadas a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , esta instrucción hace que la memoria almacenada en la memoria caché de la aplicación cliente se sincronice con el servidor. Mientras que esto normalmente se detectará y actualizará automáticamente, el período de tiempo antes de que esto suceda depende de la configuración de la cadena de conexión del cliente. La instrucción REFRESH CUBE actualiza inmediatamente los datos.  
  
 En las aplicaciones cliente conectadas a un cubo local, la instrucción REFRESH CUBE hace que el archivo de cubo local se vuelva a generar.  
  
> [!IMPORTANT]  
>  Los conjuntos con nombre que se almacenan en el servidor no se actualizan.  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de definición de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
