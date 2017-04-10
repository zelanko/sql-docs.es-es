---
title: "Copiar columna, editor de transformaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.copymaptransformation.f1"
helpviewer_keywords: 
  - "Copiar columna, editor de transformación"
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Copiar columna, editor de transformaci&#243;n
  Utilice el cuadro de diálogo **Editor de copia de transformación de columna** para seleccionar las columnas que desee copiar y para asignar nombres a las nuevas columnas de resultados.  
  
 Para obtener más información acerca de la transformación Copiar columna, vea [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md).  
  
> [!NOTE]  
>  Cuando solo copie todos los datos de origen a un destino, es posible que no sea necesario utilizar la transformación Copiar columna. En algunos escenarios, puede conectar un origen con un destino de forma directa, cuando no se requiera la transformación de datos. En estas circunstancias, por lo general, es preferible utilizar el Asistente para importación y exportación de SQL Server para crear el paquete. Después, puede mejorar y volver a configurar el paquete, si fuera necesario. Para obtener más información, vea [SQL Server Import and Export Wizard](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md).  
  
## Opciones  
 **Columnas de entrada disponibles**  
 Seleccione las columnas que desea copiar utilizando las casillas. Las selecciones agregan columnas de entrada a la tabla que aparece debajo.  
  
 **Columna de entrada**  
 Seleccione de la lista de columnas de entrada disponibles las columnas que desee copiar. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida nueva. El valor predeterminado es **Copia de**seguido del nombre de la columna de entrada; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  