---
title: Asignar parámetros de consulta a variables en un componente de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4a1d86dce6be4ed342fe8d90fefe53649533b816
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915245"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>Asignar parámetros de consulta a variables en un componente de flujo de datos
  Al configurar el origen de OLE DB para utilizar las consultas parametrizadas, puede asignar los parámetros a las variables.  
  
 El origen de OLE DB utiliza las consultas parametrizadas para filtrar los datos cuando el origen conecta con un origen de datos.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Para asignar un parámetro de consulta a una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el origen de OLE DB hasta la superficie de diseño.  
  
4.  Haga clic con el botón derecho en el origen de OLE DB y, después, haga clic en **Editar**.  
  
5.  En el **Editor de origen de OLE DB**, seleccione un administrador de conexiones OLE DB para conectarse al origen de datos o haga clic en **Nuevo** para crear un nuevo administrador de conexiones OLE DB.  
  
6.  Seleccione la opción **Comando SQL** para el modo de acceso a datos y, a continuación, escriba una consulta parametrizada en el panel **Texto de comando SQL** .  
  
7.  Haga clic en **Parámetros**.  
  
8.  En el cuadro de diálogo **establecer parámetros de consulta** , asigne cada parámetro de la lista **parámetros** a una variable de la lista **variables** o cree una nueva variable haciendo clic en **\<New variable>** . Haga clic en **OK**.  
  
    > [!NOTE]  
    >  Solo están disponibles para su asignación las variables del sistema y las variables definidas por el usuario que están en el ámbito del paquete, un contenedor principal como un bucle Foreach, o la tarea Flujo de datos que contiene el componente de flujo de datos. La variable debe tener un tipo de datos compatible con la columna en la cláusula WHERE a la que se asigna el parámetro.  
  
9. Puede hacer clic en **Vista previa** para ver hasta 200 filas de los datos que devuelve la consulta.  
  
10. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Origen de OLE DB](ole-db-source.md)   
 [Transformación Búsqueda](transformations/lookup-transformation.md)  
  
  
