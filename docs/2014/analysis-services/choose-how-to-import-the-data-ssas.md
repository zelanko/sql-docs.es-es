---
title: Elegir cómo importar los datos (SSAS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.choosehowtoimpdata.f1
ms.assetid: 17dc6903-c239-46aa-a3b0-6e3156accacc
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9929f61537fdf635ffd130b75d9e2738be256aab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203073"
---
# <a name="choose-how-to-import-the-data-ssas"></a>Elegir cómo importar los datos (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite elegir cómo importar los datos del origen de datos seleccionado. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Seleccione esta opción en una lista de tablas y vistas para elegir los datos que se va a importar**  
 Seleccione esta opción si desea importar los datos seleccionándolos en una lista.  
  
> [!NOTE]  
>  Esta opción solo está disponible cuando el origen de datos seleccionado expone información del esquema que el **Asistente para la importación de tablas** admite.  
  
 **Escribir una consulta para especificar los datos que se va a importar**  
 Seleccione esta opción si quiere importar los datos usando una consulta SQL. La consulta SQL puede tratar los datos que se importan. Por ejemplo, podría combinar los datos de tablas diferentes o seleccionar únicamente las filas que cumplan ciertos criterios.  
  
  