---
title: Configurar la transformación comando OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [Integration Services]
- OLE DB Command transformation
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a29642a667d4d22ecf5c7f6d3de0848b4725df91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254487"
---
# <a name="configure-the-ole-db-command-transformation"></a>Configurar la transformación Comando de OLE DB
  Para agregar y configurar una transformación Comando de OLE DB, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen tal como origen de archivo plano y un origen de OLE DB. Esta transformación normalmente se usa para ejecutar consultas con parámetros.  
  
### <a name="to-configure-the-ole-db-command-transformation"></a>Para configurar la transformación Comando de OLE DB  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre la transformación Comando de OLE DB a la superficie de diseño.  
  
4.  Conecte la transformación Comando de OLE DB al flujo de datos arrastrando el conector (la flecha verde o roja) desde un origen de datos o una transformación anterior a la transformación Comando de OLE DB.  
  
5.  Haga clic con el botón derecho en el componente y seleccione Editar o Mostrar el **Editor avanzado**.  
  
6.  En la pestaña **Administradores de conexión** , seleccione un administrador de conexiones OLE DB en la lista **Administrador de conexiones** . Para más información, consulte [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md).  
  
7.  Haga clic en la pestaña **Propiedades de componente** y haga clic en el botón de puntos suspensivos **(…)** en el cuadro **Comando SQL** .  
  
8.  En el **Editor de valores de cadena**, escriba la instrucción SQL con parámetros mediante un signo de pregunta (?) como marcador de parámetro para cada parámetro.  
  
9. Haga clic en **Actualizar**. Cuando hace clic en **Actualizar**, la transformación crea una columna para cada parámetro en la colección de columnas externas y establece la propiedad DBParamInfoFlags.  
  
10. Haga clic en la pestaña **Propiedades de entrada y salida** .  
  
11. Expanda **Entrada de comando de OLE DB**y luego expanda **Columnas externas**.  
  
12. Compruebe que **Columnas externas** enumera una columna para cada parámetro en la instrucción SQL. Los nombres de columna son **Param_0**, **Param_1**, etc.  
  
     No debe cambiar los nombres de las columnas. Si lo hace, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] generará un error de validación para la transformación Comando de OLE DB.  
  
     Además, tampoco debe cambiar el tipo de datos. La propiedad DataType de cada columna se establece en el tipo de datos correcto.  
  
13. Si **Columnas externas** no enumera ninguna columna, debe agregarlas manualmente.  
  
    -   Haga clic en **Agregar columna** una vez por cada parámetro de la instrucción SQL.  
  
    -   Actualice los nombres de columna a **Param_0**, **Param_1**, etc.  
  
    -   Especifique un valor en la propiedad DBParamInfoFlags. El valor debe coincidir con el valor de la enumeración OLE DB DBPARAMFLAGSENUM. Para obtener más información, vea la documentación de referencia de OLE DB.  
  
    -   Especifique el tipo de datos de la columna y, según el tipo de datos, especifique la página de códigos, longitud, precisión y escala de la columna.  
  
    -   Para eliminar un parámetro sin usar, seleccione el parámetro en **Columnas externas**y luego haga clic en **Quitar columna**.  
  
    -   Haga clic en **Asignaciones de columnas** y asigne las columnas de la lista **Columnas de entrada disponibles** a parámetros de la lista **Columnas de destino disponibles** .  
  
14. Haga clic en **Aceptar**.  
  
15. Para guardar el paquete actualizado, haga clic en **Guardar** en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Transformación comando de OLE DB](data-flow/transformations/ole-db-command-transformation.md)   
 [Transformaciones de Integration Services](data-flow/transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](data-flow/integration-services-paths.md)   
 [Tarea Flujo de datos](control-flow/data-flow-task.md)  
  
  
