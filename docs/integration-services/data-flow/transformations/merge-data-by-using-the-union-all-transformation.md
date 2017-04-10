---
title: "Combinar datos mediante la transformaci&#243;n Uni&#243;n de todo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conjuntos de datos, combinar [Integration Services]"
  - "combinar entradas [Integration Services]"
  - "combinar conjuntos de datos"
  - "Unión de todo, transformación"
  - "conjuntos de datos [Integration Services], combinar"
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Combinar datos mediante la transformaci&#243;n Uni&#243;n de todo
  Para agregar y configurar una transformación Unión de todo, el paquete ya debe incluir al menos una tarea Flujo de datos y dos orígenes de datos.  
  
 La transformación Unión de todo combina varias entradas. La primera entrada que se conecta con la transformación es la entrada de referencia y las entradas conectadas posteriormente son las entradas secundarias. La salida incluye las columnas en la entrada de referencia.  
  
### Para combinar entradas en un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], haga doble clic en el paquete del Explorador de soluciones para abrir el paquete en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] y, después, haga clic en la pestaña **Flujo de datos**.  
  
2.  Desde el **cuadro de herramientas**, arrastre la transformación Unión de todo a la superficie de diseño de la pestaña **Flujo de datos** .  
  
3.  Conecte la transformación Unión de todo al flujo de datos arrastrando un conector desde el origen de datos o una transformación anterior a la transformación Unión de todo.  
  
4.  Haga doble clic en la transformación Unión de todo.  
  
5.  En el **Editor de transformación Unión de todo**, asigne una columna de una entrada a una columna en la lista **Nombre de la columna de salida** haciendo clic en una fila y luego seleccionando una columna en la lista de entrada. Seleccione **\<omitir>** en la lista de entrada para omitir la asignación de la columna.  
  
    > [!NOTE]  
    >  La asignación entre dos columnas requiere que los metadatos de las columnas coincidan.  
  
    > [!NOTE]  
    >  Las columnas en una entrada secundaria que no se asignan a las columnas de referencia se establecen con valores NULL en la salida.  
  
6.  Opcionalmente, modifique los nombres de las columnas en la columna **Nombre de la columna de salida** .  
  
7.  Repita los pasos 5 y 6 para cada columna en cada entrada.  
  
8.  Haga clic en **Aceptar**.  
  
9. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## Vea también  
 [Transformación Unión de todo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarea Flujo de datos](../../../integration-services/control-flow/data-flow-task.md)  
  
  