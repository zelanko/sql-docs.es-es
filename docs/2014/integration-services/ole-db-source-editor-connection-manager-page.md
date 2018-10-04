---
title: Editor de origen de OLE DB (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c25e36d44b4b088bb2874039d4c292d76759da73
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172985"
---
# <a name="ole-db-source-editor-connection-manager-page"></a>Editor de origen de OLE DB (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de OLE DB** para seleccionar el administrador de conexiones OLE DB para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
> [!NOTE]  
>  Para cargar datos desde un origen de datos que use [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2007, use un origen de OLE DB. No puede usar un origen de Excel para cargar datos desde un origen de datos de Excel 2007. Para más información, consulte [Configure OLE DB Connection Manager](configure-ole-db-connection-manager.md).  
>   
>  Para cargar datos desde un origen de datos que use [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2003 o anterior, use un origen de Excel. Para más información, vea [Editor de origen de Excel &#40;página Administrador de conexiones&#41;](../../2014/integration-services/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  El `CommandTimeout` propiedad del origen de OLE DB no está disponible en el **Editor de origen de OLE DB**, pero se puede establecer utilizando la **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md).  
  
 Para obtener más información acerca del origen de OLE DB, vea [OLE DB Source](data-flow/ole-db-source.md).  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Abrir el Editor de origen de OLE DB (página Administrador de conexiones)  
  
1.  Agregue el origen de OLE DB al paquete [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente de origen y, después, haga clic en **Editar**.  
  
3.  Haga clic en **Administrador de conexiones**.  
  
## <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OLE DB**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones con el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tabla o vista|Obtenga datos de una tabla o vista en el origen de datos OLE DB.|  
|Variable de nombre de tabla o nombre de vista|Especifique el nombre de la tabla o vista de una variable.<br /><br /> **Información relacionada:** [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Obtenga datos del origen de datos OLE DB mediante una consulta SQL.|  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . **Vista previa** puede mostrar hasta 200 filas.  
  
> [!NOTE]  
>  Cuando genera una vista previa de datos, las columnas con un tipo definido por el usuario CLR no contienen datos. En su lugar, se muestran los valores \<value too big to display> o System.Byte[]. El primero se muestra cuando se tiene acceso al origen de datos mediante el proveedor SQL OLE DB y el último, cuando se utiliza el proveedor Native Client [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
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
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de OLE DB &#40;página columnas&#41;](../../2014/integration-services/ole-db-source-editor-columns-page.md)   
 [Editor de origen de OLE DB &#40;página de salida de Error&#41;](../../2014/integration-services/ole-db-source-editor-error-output-page.md)   
 [Extraer datos mediante el origen de OLE DB](data-flow/extract-data-by-using-the-ole-db-source.md)   
 [Administrador de conexiones OLE DB](connection-manager/ole-db-connection-manager.md)  
  
  
