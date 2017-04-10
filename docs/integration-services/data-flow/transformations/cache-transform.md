---
title: "Transformaci&#243;n de cach&#233; | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.cachetrans.f1"
helpviewer_keywords: 
  - "Transformación de caché"
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Transformaci&#243;n de cach&#233;
  La transformación de caché genera un conjunto de datos de referencia para la transformación de búsqueda escribiendo datos de un origen de datos conectado del flujo de datos en un Administrador de conexiones de caché. La transformación Búsqueda realiza búsquedas mediante la combinación de datos de las columnas de entrada procedentes de un origen de datos conectado con columnas de la base de datos de referencia.  
  
 Puede usar el Administrador de conexiones de caché si desea configurar la transformación Búsqueda para que se ejecute en modo de caché completa. En este modo, el conjunto de datos de referencia se carga en la memoria caché antes de que se ejecute la transformación Búsqueda.  
  
 Para obtener instrucciones sobre cómo configurar la transformación Búsqueda en modo de caché completa con el Administrador de conexiones de caché y la transformación de caché, vea [Implementar una transformación de búsqueda en el modo de caché completa mediante el Administrador de conexiones de caché](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - cache connection manager.md).  
  
 Para obtener más información acerca del almacenamiento en memoria caché del conjunto de datos de referencia, vea [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
> [!NOTE]  
>  La transformación de caché solo escribe filas únicas en el administrador de conexiones de caché.  
  
 En un paquete único, solo una transformación de caché puede escribir datos en el mismo administrador de conexiones de caché. Si el paquete contiene varias transformaciones de caché, la primera transformación de caché a la que se llama cuando se ejecuta el paquete escribe los datos en el administrador de conexiones. Las operaciones de escritura de las transformaciones de caché posteriores producirán errores.  
  
 Para obtener más información, consulte [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) y [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).  
  
## Configuración de la transformación de caché  
 Puede configurar el administrador de conexiones de caché para guardar los datos en un archivo caché (.caw).  
  
 Puede configurar la transformación de caché de las siguientes maneras:  
  
-   Especificar el administrador de conexiones de caché.  
  
-   Asignar columnas de entrada de la transformación de caché a columnas de destino del administrador de conexiones de caché.  
  
    > [!NOTE]  
    >  Cada columna de entrada debe estar asignada a una columna de destino y los tipos de datos de columna deben ser iguales. De lo contrario, el Diseñador [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] muestra un mensaje de error.  
  
     Puede utilizar el **Editor del administrador de conexiones de caché** para modificar tipos de datos y nombres de columna, y otras propiedades de columna.  
  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Para obtener más información acerca de las propiedades que se pueden establecer en el cuadro de diálogo **Editor avanzado** , vea [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Para obtener más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Vea también  
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)  
  
  