---
title: Copie el Editor de transformación de columna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- Copy Column Transformation Editor
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 62f2811fb25311ab6aab23d4af66b59befb6611b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227767"
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
  
  
