---
title: Editor de origen de Excel (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsourceadapter.connection.f1
helpviewer_keywords:
- Excel Source Editor
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c3132bd65bb6f3092cc950758d4f346b5c4cd8fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059169"
---
# <a name="excel-source-editor-connection-manager-page"></a>Editor de origen de Excel (página Administrador de conexiones)
  Utilice el nodo **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel** para seleccionar el libro de [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] que utilizará el origen. El origen de Excel lee los datos de una hoja de cálculo o un rango con nombre de un libro existente.  
  
> [!NOTE]  
>  La `CommandTimeout` propiedad del origen de Excel no está disponible en el **Editor de origen de Excel**, pero se puede establecer mediante el **editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [Excel Custom Properties](data-flow/excel-custom-properties.md).  
  
 Para obtener más información acerca del origen de Excel, vea [Excel Source](data-flow/excel-source.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones de OLE DB**  
 Seleccione un Administrador de conexiones con Excel en la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nuevo**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Tabla o vista|Recupera los datos de una hoja de cálculo o un rango con nombre del archivo Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada:** [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Recupera datos del archivo Excel mediante una consulta SQL. Para obtener información acerca de la sintaxis de consultas, vea [Excel Source](data-flow/excel-source.md).|  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el libro de Excel.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de la variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien examine el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Parámetros**  
 Si ha escrito una consulta con parámetros mediante ? como marcador de posición de parámetro en el texto de la consulta, utilice el cuadro de diálogo **Establecer parámetros de consulta** para asignar los parámetros de entrada de las consultas a las variables del paquete.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acceso a datos = Comando SQL de variable  
 **Nombre de la variable**  
 Seleccione la variable que contiene el texto de la consulta SQL.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de Excel &#40;página columnas&#41;](../../2014/integration-services/excel-source-editor-columns-page.md)   
 [Editor de origen de Excel &#40;página salida de error&#41;](../../2014/integration-services/excel-source-editor-error-output-page.md)   
 [Administrador de conexiones con Excel](connection-manager/excel-connection-manager.md)   
 [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](control-flow/foreach-loop-container.md)  
  
  
