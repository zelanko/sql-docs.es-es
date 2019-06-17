---
title: Editor de origen de ADO NET (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.connection.f1
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f3d9d2270603c3f38189478ccaaf48510085907f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061687"
---
# <a name="ado-net-source-editor-connection-manager-page"></a>Editor de orígenes de ADO NET (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de orígenes de ADO NET** para seleccionar el administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 Para obtener más información acerca del origen de ADO NET, vea [ADO NET Source](data-flow/ado-net-source.md).  
  
 **Para abrir la página Administrador de conexiones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que tiene el origen de ADO NET.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de ADO NET.  
  
3.  En el **Editor de orígenes de ADO NET**, haga clic en **Administrador de conexiones**.  
  
## <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones de ADO.NET**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tabla o vista|Recupera datos de una tabla o vista del origen de datos [!INCLUDE[vstecado](../includes/vstecado-md.md)] .|  
|Comando SQL|Recupera datos del origen de datos [!INCLUDE[vstecado](../includes/vstecado-md.md)] mediante una consulta SQL.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . **Vista previa** puede mostrar hasta 200 filas.  
  
> [!NOTE]  
>  Cuando genera una vista previa de datos, las columnas con un tipo definido por el usuario CLR no contienen datos. En su lugar, se muestran los valores \<value too big to display> o System.Byte[]. El primero se muestra cuando se tiene acceso al origen de datos mediante el proveedor [!INCLUDE[vstecado](../includes/vstecado-md.md)] y el último, cuando se utiliza el proveedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
## <a name="see-also"></a>Vea también  
 [Editor de orígenes de ADO NET &#40;página Columnas&#41;](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [Editor de orígenes de ADO NET &#40;página Salida de error&#41;](../../2014/integration-services/ado-net-source-editor-error-output-page.md)   
 [Administrador de conexiones ADO.NET](connection-manager/ado-net-connection-manager.md)  
  
  
