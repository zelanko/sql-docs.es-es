---
title: "Administrador de conexiones de cach&#233; | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Administrador de conexiones de caché"
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Administrador de conexiones de cach&#233;
  El administrador de conexiones de caché lee datos a partir de la transformación de caché o de un archivo caché (.caw) y puede guardar los datos en un archivo caché. Si configura el administrador de conexiones de caché para que utilice un archivo caché, los datos siempre se almacenan en memoria.  
  
 La transformación de caché escribe los datos procedentes de un origen de datos conectado del flujo de datos en un administrador de conexiones de caché. La transformación Búsqueda de un paquete realiza búsquedas en los datos.  
  
> [!NOTE]  
>  El administrador de conexiones de caché no admite los tipos de datos de objetos binarios grandes (BLOB) DT_TEXT, DT_NTEXT y DT_IMAGE. Si el conjunto de datos de referencia contiene un tipo de datos BLOB, se producirá un error en el componente al ejecutar el paquete. Puede utilizar el **Editor del administrador de conexiones de caché** para modificar los tipos de datos de columna. Para obtener más información, vea [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).  
  
> [!NOTE]  
>  El nivel de protección del paquete no se aplica al archivo caché. Si el archivo caché contiene información confidencial, utilice una lista de control de acceso (ACL) para restringir el acceso a la ubicación o carpeta en la que almacena el archivo. Solo debería permitir el acceso a ciertas cuentas. Para más información, vea [Acceso a los archivos usados por los paquetes](../../../integration-services/security/access-to-files-used-by-packages.md).  
  
## Configuración del administrador de conexiones de caché  
 Puede configurar el administrador de conexiones de caché de las siguientes maneras:  
  
-   Indicar si se ha de utilizar un archivo caché.  
  
     Si configura el administrador de conexiones de caché para utilizar un archivo caché, el administrador de conexiones realizará una de las siguientes acciones:  
  
    -   Guardar los datos en el archivo cuando se haya configurado una transformación de caché para escribir los datos procedentes de un origen de datos del flujo de datos en el administrador de conexiones de caché.  
  
    -   Leer los datos desde el archivo caché.  
  
     Para obtener más información, vea [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Cambiar los metadatos de las columnas almacenadas en la caché.  
  
-   Actualizar el nombre del archivo caché en tiempo de ejecución con una expresión para establecer la propiedad ConnectionString. Para más información, vea [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede configurar en el Diseñador [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , vea [Editor del administrador de conexiones de caché](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).  
  
 Para más información sobre cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Tareas relacionadas  
 [Implementar una transformación de búsqueda en el modo de caché completa mediante el Administrador de conexiones de caché](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - cache connection manager.md)  
  
  