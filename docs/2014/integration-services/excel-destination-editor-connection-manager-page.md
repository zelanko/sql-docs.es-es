---
title: Editor de destino de Excel (página Administrador de conexiones) | Documentos de Microsoft
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
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 14b06c895b60f3965d7b7ccd0bea5c3d6f8b447b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197657"
---
# <a name="excel-destination-editor-connection-manager-page"></a>Editor de destino de Excel (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de Excel** para especificar la información de orígenes de datos y para obtener una vista previa de los resultados. El destino de Excel carga los datos en una hoja de cálculo o en un rango con nombre de un libro de [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  El `CommandTimeout` propiedad del destino Excel no está disponible en la **Editor de destino de Excel**, pero se puede establecer mediante el uso de la **Editor avanzado**. Además, ciertas opciones de carga rápida solo están disponibles en el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el destino de Excel en [Excel Custom Properties](data-flow/excel-custom-properties.md).  
  
 Para obtener más información acerca del destino de Excel, vea [Excel Destination](data-flow/excel-destination.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones con Excel**  
 Seleccione un Administrador de conexiones con Excel en la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tabla o vista|Carga datos en una hoja de cálculo o en un rango con nombre del origen de datos de Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Cargue datos en el destino de Excel utilizando una consulta SQL.|  
  
 **Nombre de la hoja de Excel**  
 Seleccione el destino de Excel de la lista desplegable. Si la lista está vacía, haga clic en **Nuevo**.  
  
 **Nueva**  
 Haga clic en **Nuevo** para iniciar el cuadro de diálogo **Crear tabla** . Al hacer clic en **Aceptar**, el cuadro de diálogo crea el archivo de Excel al que señala el **Administrador de conexiones con Excel** .  
  
 **Datos existentes de la vista**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta** . La vista previa puede mostrar hasta 200 filas.  
  
> [!WARNING]  
>  Si el **Administrador de conexiones con Excel** que ha seleccionado apunta a un archivo de Excel que no existe, verá un mensaje de error al hacer clic en este botón.  
  
## <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el origen de datos.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de Excel &#40;página asignaciones&#41;](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [Editor de destino de Excel &#40;página de salida de Error&#41;](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [Crear bucles entre archivos y tablas de Excel mediante un contenedor de bucles ForEach](control-flow/foreach-loop-container.md)  
  
  