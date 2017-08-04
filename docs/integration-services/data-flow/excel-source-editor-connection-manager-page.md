---
title: "Editor de origen de Excel (página Administrador de conexiones) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsourceadapter.connection.f1
helpviewer_keywords:
- Excel Source Editor
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1f01be71a5093945a49c43a3a2aec334db7584b
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="excel-source-editor-connection-manager-page"></a>Editor de origen de Excel (página Administrador de conexiones)
  Utilice el nodo **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel** para seleccionar el libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] que utilizará el origen. El origen de Excel lee los datos de una hoja de cálculo o un rango con nombre de un libro existente.  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del origen de Excel no está disponible en el **Editor de origen de Excel**, pero se puede establecer mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
 Para obtener más información acerca del origen de Excel, vea [Excel Source](../../integration-services/data-flow/excel-source.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **OLE DB, administrador de conexiones**  
 Seleccione un administrador de conexiones de Excel en la lista o cree una nueva conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Value|Description|  
|-----------|-----------------|  
|Tabla o vista|Recupera los datos de una hoja de cálculo o un rango con nombre del archivo Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada** [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Recupera datos del archivo Excel mediante una consulta SQL. Para obtener información acerca de la sintaxis de consultas, vea [Excel Source](../../integration-services/data-flow/excel-source.md).|  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el libro de Excel.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien examine el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Parámetros**  
 Si ha escrito una consulta con parámetros mediante ? como marcador de posición de parámetro en el texto de la consulta, utilice el cuadro de diálogo **Establecer parámetros de consulta** para asignar los parámetros de entrada de las consultas a las variables del paquete.  
  
 **Build query**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acceso a datos = Comando SQL de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene el texto de la consulta SQL.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de Excel &#40; Página columnas &#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Editor de origen de Excel &#40; Página de salida de error &#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Administrador de conexiones de Excel](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Bucle a través de Excel, archivos y tablas mediante el uso de un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
