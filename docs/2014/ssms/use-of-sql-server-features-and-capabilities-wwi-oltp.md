---
title: Argumentos para herramientas externas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a568423d865e9ffea07f4e4487ea6d3680e2b417
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198824"
---
# <a name="arguments-for-external-tools"></a>Arguments for External Tools
  Los argumentos son variables para las que el entorno de Studio proporciona valores cuando se inicia una herramienta desde el menú **Herramientas** . Es posible agregar herramientas externas, como el Bloc de notas, al menú **Herramientas** mediante el cuadro de diálogo **Herramientas externas** .  
  
 En la tabla siguiente se enumeran los argumentos de las herramientas externas.  
  
|Nombre|Argumento|Descripción|  
|----------|--------------|-----------------|  
|**Ruta de acceso del elemento**|$(ItemPath)|El nombre completo del archivo de origen actual (definido como unidad + ruta de acceso + nombre de archivo); en blanco si hay una ventana de no origen activa.|  
|**Directorio del elemento**|$(ItemDir)|El directorio del origen actual (definido como unidad + ruta de acceso); en blanco si hay una ventana de no origen activa.|  
|**Nombre de archivo del elemento**|$(ItemFilename)|El nombre del archivo de origen actual (definido como nombre de archivo); en blanco si hay una ventana de no origen activa.|  
|**Extensión del elemento**|$(ItemExt)|La extensión del nombre del archivo de origen actual.|  
|**Línea actual** <sup>1</sup>|$(CurLine)|La posición actual en la línea del cursor en el editor.|  
|**Columna actual**1|$(CurCol)|La posición actual en la columna del cursor en el editor.|  
|**Texto actual**1|$(CurText)|El texto actual (la palabra en la que se encuentra el cursor o una selección de una única línea, si la hay).|  
|**Ruta de acceso de destino**|$(TargetPath)|El nombre completo del archivo de destino (definido como unidad + ruta de acceso + nombre de archivo).|  
|**Directorio de destino**|$(TargetDir)|El directorio del archivo de destino.|  
|**Nombre de destino**|$(TargetName)|El nombre del archivo de destino.|  
|**Extensión de destino**|$(TargetExt)|La extensión del nombre del archivo de destino.|  
|**Directorio del proyecto**|$(ProjDir)|El directorio del proyecto actual (definido como unidad + ruta de acceso).|  
|**Nombre de archivo del proyecto**|$(ProjFileName)|El nombre de archivo del proyecto actual (definido como unidad + ruta de acceso + nombre de archivo).|  
|**Directorio de la solución**|$(SolutionDir)|El directorio de la solución actual (definido como unidad + ruta de acceso).|  
|**Nombre de archivo de la solución**|$(SolutionFileName)|El nombre de archivo de la solución actual (definido como unidad + ruta de acceso + nombre de archivo).|  
  
 <sup>1</sup> la línea actual, la columna actual o el texto actual se basa en la posición del cursor en el editor de texto, como se muestra en la barra de estado.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo Herramientas externas](external-tools-dialog-box.md)   
 [Elementos generales de la interfaz de usuario](general-user-interface-elements.md)  
  
  