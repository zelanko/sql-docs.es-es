---
title: Argumentos para herramientas externas | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c09b8aa81f0846305b0bd1f33a89a269af64b45
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="arguments-for-external-tools"></a>Argumentos de las herramientas externas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Los argumentos son variables para las que el entorno de Studio proporciona valores cuando se inicia una herramienta desde el menú **Herramientas**. Es posible agregar herramientas externas, como el Bloc de notas, al menú **Herramientas** mediante el cuadro de diálogo **Herramientas externas** .  
  
En la tabla siguiente se enumeran los argumentos de las herramientas externas.  
  
|Nombre|Argumento|Description|  
|--------|------------|---------------|  
|**Ruta de acceso del elemento**|$(ItemPath)|El nombre completo del archivo de origen actual (definido como unidad + ruta de acceso + nombre de archivo); en blanco si hay una ventana de no origen activa.|  
|**Directorio del elemento**|$(ItemDir)|El directorio del origen actual (definido como unidad + ruta de acceso); en blanco si hay una ventana de no origen activa.|  
|**Nombre de archivo del elemento**|$(ItemFilename)|El nombre del archivo de origen actual (definido como nombre de archivo); en blanco si hay una ventana de no origen activa.|  
|**Extensión del elemento**|$(ItemExt)|La extensión del nombre del archivo de origen actual.|  
|**Línea actual***|$(CurLine)|La posición actual en la línea del cursor en el editor.|  
|**Columna actual***|$(CurCol)|La posición actual en la columna del cursor en el editor.|  
|**Texto actual***|$(CurText)|El texto actual (la palabra en la que se encuentra el cursor o una selección de una única línea, si la hay).|  
|**Ruta de acceso de destino**|$(TargetPath)|El nombre completo del archivo de destino (definido como unidad + ruta de acceso + nombre de archivo).|  
|**Directorio de destino**|$(TargetDir)|El directorio del archivo de destino.|  
|**Nombre de destino**|$(TargetName)|El nombre del archivo de destino.|  
|**Extensión de destino**|$(TargetExt)|La extensión del nombre del archivo de destino.|  
|**Directorio del proyecto**|$(ProjDir)|El directorio del proyecto actual (definido como unidad + ruta de acceso).|  
|**Nombre de archivo del proyecto**|$(ProjFileName)|El nombre de archivo del proyecto actual (definido como unidad + ruta de acceso + nombre de archivo).|  
|**Directorio de la solución**|$(SolutionDir)|El directorio de la solución actual (definido como unidad + ruta de acceso).|  
|**Nombre de archivo de la solución**|$(SolutionFileName)|El nombre de archivo de la solución actual (definido como unidad + ruta de acceso + nombre de archivo).|  
  
*La línea actual, la columna actual o el texto actual se basan en la posición del cursor en el editor de texto tal y como aparece en la barra de estado.  
  
## <a name="see-also"></a>Vea también  
[Cuadro de diálogo Herramientas externas](../ssms/external-tools-dialog-box.md)  
[Elementos generales de la interfaz de usuario](../ssms/general-user-interface-elements.md)  
  
