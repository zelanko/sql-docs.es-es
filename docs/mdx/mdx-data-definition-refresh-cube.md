---
title: Instrucción REFRESH CUBE (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f27051d9e0fe1d0a6eb3d580548233eb9f073215
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579777"
---
# <a name="mdx-data-definition---refresh-cube"></a>Definición de datos MDX - actualización de cubo
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Actualiza la caché de cliente para un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que proporciona un nombre de cubo.  
  
## <a name="remarks"></a>Notas  
 Para las aplicaciones cliente conectadas a una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], esta instrucción hace que la memoria caché en la aplicación cliente se sincronicen con el servidor. Mientras que esto normalmente se detectará y actualizará automáticamente, el período de tiempo antes de que esto suceda depende de la configuración de la cadena de conexión del cliente. La instrucción REFRESH CUBE actualiza inmediatamente los datos.  
  
 En las aplicaciones cliente conectadas a un cubo local, la instrucción REFRESH CUBE hace que el archivo de cubo local se vuelva a generar.  
  
> [!IMPORTANT]  
>  Los conjuntos con nombre que se almacenan en el servidor no se actualizan.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
