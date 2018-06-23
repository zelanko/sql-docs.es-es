---
title: Copiar columna, Editor de transformación | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- Copy Column Transformation Editor
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 361e0426e4101a281bfb302dad8f4b9d4cc5ded9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104296"
---
# <a name="copy-column-transformation-editor"></a>Copiar columna, editor de transformación
  Utilice el cuadro de diálogo **Editor de copia de transformación de columna** para seleccionar las columnas que desee copiar y para asignar nombres a las nuevas columnas de resultados.  
  
 Para obtener más información acerca de la transformación Copiar columna, vea [Copy Column Transformation](data-flow/transformations/copy-column-transformation.md).  
  
> [!NOTE]  
>  Cuando solo copie todos los datos de origen a un destino, es posible que no sea necesario utilizar la transformación Copiar columna. En algunos escenarios, puede conectar un origen con un destino de forma directa, cuando no se requiera la transformación de datos. En estas circunstancias, por lo general, es preferible utilizar el Asistente para importación y exportación de SQL Server para crear el paquete. Después, puede mejorar y volver a configurar el paquete, si fuera necesario. Para obtener más información, vea [SQL Server Import and Export Wizard](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Seleccione las columnas que desea copiar utilizando las casillas. Las selecciones agregan columnas de entrada a la tabla que aparece debajo.  
  
 **Columna de entrada**  
 Seleccione de la lista de columnas de entrada disponibles las columnas que desee copiar. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida nueva. El valor predeterminado es **Copia de**seguido del nombre de la columna de entrada; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  