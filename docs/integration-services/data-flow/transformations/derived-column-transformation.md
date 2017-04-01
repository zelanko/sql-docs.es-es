---
title: "Transformaci&#243;n Columna derivada | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.derivedcolumntrans.f1"
helpviewer_keywords: 
  - "varias columnas derivadas"
  - "expresiones [Integration Services], columnas derivadas"
  - "derivadas, columnas"
  - "columnas [Integration Services], derivaciones"
  - "Transformación Columna derivada"
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
caps.latest.revision: 60
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 60
---
# Transformaci&#243;n Columna derivada
  La transformación Columna derivada crea nuevos valores de columna aplicando expresiones a las columnas de entrada de la transformación. Una expresión puede contener cualquier combinación variables, funciones, operadores y columnas de la entrada de transformación. El resultado puede agregarse como una nueva columna o insertarse en una columna existente como un valor de reemplazo. La transformación Columna derivada puede definir varias columnas derivadas, y cualquier variable o columna de entrada puede aparecer en varias expresiones.  
  
 Puede utilizar esta transformación para realizar las siguientes tareas:  
  
-   Concatenar datos de distintas columnas en una columna derivada. Por ejemplo, puede combinar valores de las columnas **FirstName** y **LastName** en una sola columna derivada, denominada **FullName**, mediante la expresión `FirstName + " " + LastName`.  
  
-   Extraer caracteres de datos de cadena mediante funciones como SUBSTRING y después almacenar el resultado en una columna derivada. Por ejemplo, puede extraer de la columna **FirstName** la inicial del nombre de una persona mediante la expresión `SUBSTRING(FirstName,1,1)`.  
  
-   Aplicar funciones matemáticas a datos numéricos y almacenar el resultado en una columna derivada. Por ejemplo, puede cambiar la longitud y la precisión de una columna numérica, **SalesTax**, a un número con dos cifras decimales mediante la expresión `ROUND(SalesTax, 2)`.  
  
-   Crear expresiones que comparen columnas de entrada y variables. Por ejemplo, puede comparar la variable **Version** con los datos de la columna **ProductVersion**y, en función del resultado de la comparación, usar el valor de **Version** o **ProductVersion**mediante la expresión `ProductVersion == @Version? ProductVersion : @Version`.  
  
-   Extraer partes de un valor datetime. Por ejemplo, puede utilizar las funciones GETDATE y DATEPART para extraer el año actual mediante la expresión `DATEPART("year",GETDATE())`.  
  
-   Convierta las cadenas de fecha a un formato específico mediante una expresión.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>Configuración de la transformación Columna derivada  
 Puede configurar la transformación Columna derivada de las maneras siguientes:  
  
-   Proporcionar una expresión para cada columna de entrada o nueva columna que se vaya a modificar. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Si una expresión hace referencia a una columna de entrada sobrescrita por la transformación Columna derivada, la expresión utiliza el valor original de la columna, no el valor derivado.  
  
-   Si agrega resultados a columnas nuevas y el tipo de datos es **string**, especifique una página de códigos. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 La transformación Columna derivada incluye la propiedad personalizada FriendlyExpression. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para obtener más información, vea [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md)y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada, una salida normal y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Columna derivada** , vea [Derived Column Transformation Editor](../../../integration-services/data-flow/transformations/derived-column-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../Topic/Common%20Properties.md)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
-   [Derivar valores de columna mediante la transformación Columna derivada](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo técnico, sobre [ejemplos de expresiones SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
