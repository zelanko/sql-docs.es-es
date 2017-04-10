---
title: "Editor de destino de Excel (p&#225;gina Administrador de conexiones) | Microsoft Docs"
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
  - "sql13.dts.designer.exceldestadapter.connection.f1"
helpviewer_keywords: 
  - "destino de Excel, editor de"
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Editor de destino de Excel (p&#225;gina Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de Excel** para especificar la información de orígenes de datos y para obtener una vista previa de los resultados. El destino de Excel carga los datos en una hoja de cálculo o en un rango con nombre de un libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del destino de Excel no está disponible en el **Editor de destino de Excel**, pero se puede establecer mediante el **Editor avanzado**. Además, ciertas opciones de carga rápida solo están disponibles en el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el destino de Excel en [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
 Para obtener más información acerca del destino de Excel, vea [Excel Destination](../../integration-services/data-flow/excel-destination.md).  
  
## Opciones estáticas  
 **Administrador de conexiones con Excel**  
 Seleccione un Administrador de conexiones con Excel en la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nuevo**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel**.  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Description|  
|------------|-----------------|  
|Tabla o vista|Carga datos en una hoja de cálculo o en un rango con nombre del origen de datos de Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Comando SQL|Cargue datos en el destino de Excel utilizando una consulta SQL.|  
  
 **Nombre de la hoja de Excel**  
 Seleccione el destino de Excel de la lista desplegable. Si la lista está vacía, haga clic en **Nuevo**.  
  
 **Nuevo**  
 Haga clic en **Nuevo** para iniciar el cuadro de diálogo **Crear tabla**. Al hacer clic en **Aceptar**, el cuadro de diálogo crea el archivo de Excel al que señala el **Administrador de conexiones con Excel** .  
  
 **Datos existentes de la vista**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta**. La vista previa puede mostrar hasta 200 filas.  
  
> [!WARNING]  
>  Si el **Administrador de conexiones con Excel** que ha seleccionado apunta a un archivo de Excel que no existe, verá un mensaje de error al hacer clic en este botón.  
  
## Opciones dinámicas del modo de acceso a datos  
  
### Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el origen de datos.  
  
### Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
### Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para encontrar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de Excel &#40;página Asignaciones&#41;](../../integration-services/data-flow/excel-destination-editor-mappings-page.md)   
 [Editor de destino de Excel &#40;página Salida de error&#41;](../../integration-services/data-flow/excel-destination-editor-error-output-page.md)   
 [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  