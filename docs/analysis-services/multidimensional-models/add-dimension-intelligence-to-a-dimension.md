---
title: "Agregar inteligencia de dimensiones a una dimensi&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mejoras de Business Intelligence [Analysis Services], inteligencia de dimensión"
  - "dimensiones [Analysis Services], mejoras de Business Intelligence"
  - "inteligencia de dimensiones [Analysis Services]"
  - "Type, propiedad"
ms.assetid: b64fa386-eac2-4286-a320-0631a1887aac
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Agregar inteligencia de dimensiones a una dimensi&#243;n
  Agregar la mejora de inteligencia de dimensiones a un cubo o dimensión para especificar un tipo de negocio estándar para una dimensión. Esta mejora también especifica los tipos correspondientes para los atributos de dimensión. Las aplicaciones cliente pueden utilizar estas especificaciones de tipos al analizar datos.  
  
 Para agregar la inteligencia de dimensiones, use el Asistente de Business Intelligence y seleccione la opción **Definir la inteligencia de dimensiones** en la página **Elegir mejora** . A continuación, este asistente le guía por los pasos de la selección de una dimensión a la que desee aplicar la inteligencia de dimensiones e identificar los atributos para la dimensión seleccionada.  
  
## Seleccionar una dimensión  
 En la primera página del asistente, **Establecer las opciones de la inteligencia de dimensiones** , se especifica la dimensión a la que se desea aplicar la inteligencia de dimensiones. La mejora de inteligencia de dimensiones agregada a esta dimensión seleccionada produce cambios en la dimensión. Estos cambios son heredados por todos los cubos que incluyan la dimensión seleccionada.  
  
> [!NOTE]  
>  Si se selecciona **Cuenta** como la dimensión, se especifica la inteligencia de cuenta para la dimensión. Para obtener más información, vea [Agregar inteligencia de cuentas a una dimensión](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Especificar atributos de dimensión  
 En la página **Definir la inteligencia de dimensiones** , en la lista **Tipo de dimensión** , la selección realizada establece la propiedad **Type** de la dimensión. La configuración de la propiedad **Type** proporciona información a los servidores y aplicaciones cliente sobre el contenido de una dimensión. Algunas configuraciones solo proporcionan instrucciones para aplicaciones cliente; estas configuraciones son opcionales. Otras configuraciones, como Cuentas o Tiempo, determinan comportamientos específicos y pueden ser necesarias para implementar mejoras específicas de inteligencia empresarial. Por ejemplo, SQL Server Management Studio usa el tipo de dimensión para identificar una dimensión de Moneda y establecer las normas pertinentes de conversión de moneda. La configuración predeterminada para **Tipo de dimensión** es **Normal**, que no hace suposiciones sobre el contenido de la dimensión.  
  
 Después de seleccionar el tipo de dimensión en **Atributos de dimensión**, en la columna **Incluir** , active la casilla situada junto a cada tipo de atributo estándar para el que haya un atributo correspondiente en la dimensión. Finalmente, en la columna **Atributo de dimensión**, expanda la lista desplegable y seleccione el atributo en la dimensión que corresponde al tipo de atributo seleccionado. Seleccionar el atributo de la lista establece la propiedad **Type** del atributo para los atributos.  
  
 Por ejemplo, desea agregar inteligencia de dimensiones a una dimensión Cuentas. En **Tipo de dimensión**, seleccione **Cuentas**. Entonces, si la dimensión tiene los atributos **Tipo de cuenta** y **Descripción de cuenta** , en la columna **Incluir** , active las casillas para los tipos de cuenta **Nombre de cuenta** y **Tipo de cuenta** . A continuación, en la columna **Atributo de dimensión** , asocie estos tipos de cuenta con los atributos **Descripción de cuenta** y **Tipo de cuenta** , respectivamente, en la dimensión.  
  
## Vea también  
 [Definir cálculos de inteligencia de tiempo mediante el Asistente de Business Intelligence](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  