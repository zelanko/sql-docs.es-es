---
description: 'Lección 1-3: Adición y configuración de un administrador de conexiones OLE DB'
title: 'Paso 3: Adición y configuración de un administrador de conexiones OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 33eeb6e462c096505fc4fbd1088e7f5b36b37618
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449709"
---
# <a name="lesson-1-3-add-and-configure-an-ole-db-connection-manager"></a>Lección 1-3: Adición y configuración de un administrador de conexiones OLE DB

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Después de agregar un administrador de conexiones de archivos planos al origen de datos, se agrega un administrador de conexiones OLE DB para conectarse al destino de datos. Un administrador de conexiones OLE DB permite a un paquete extraer datos de un origen de datos compatible con OLE DB o cargar datos en este origen de datos. Mediante un administrador de conexiones OLE DB, puede especificar el servidor, el método de autenticación y la base de datos predeterminada de la conexión.  
  
En esta tarea, creará un administrador de conexiones OLE DB que usa la Autenticación de Windows para conectarse a la instancia local de **AdventureWorksDW2012**. Otros componentes que creará más adelante en este tutorial, como la transformación Búsqueda y el destino de OLE DB, también hacen referencia a este administrador de conexiones OLE DB.  
  
## <a name="add-and-configure-an-ole-db-connection-manager"></a>Adición y configuración de un administrador de conexiones OLE DB

1. Haga clic con el botón derecho en **Administradores de conexiones** en el **Explorador de soluciones** y, después, seleccione **Nuevo administrador de conexiones**.

1. En el cuadro de diálogo **Agregar administrador de conexiones SSIS**, seleccione **OLEDB** y, después, haga clic en **Agregar**.
    
2. En el cuadro de diálogo **Configurar el administrador de conexiones OLE DB**, haga clic en **Nuevo**.  
  
3. En **Nombre del servidor**, escriba **localhost**.  
  
    Cuando se especifica localhost como el nombre del servidor, el administración de conexión se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo local. Para usar una instancia remota de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sustituya localhost con el nombre del servidor al que desea conectarse.  
  
4. En el grupo **Iniciar sesión en el servidor** , compruebe que la opción **Usar autenticación de Windows** está seleccionada.  
  
5. En el grupo **Conectar con una base de datos** , en el cuadro **Seleccione o escriba un nombre de base de datos** , escriba o seleccione **AdventureWorksDW2012**.  
  
6. Haga clic en **Probar conexión** para comprobar si los parámetros de conexión que ha especificado son válidos.  
  
7. Seleccione **Aceptar**.  
  
8. Seleccione **Aceptar**.  
  
9. En el panel **Administradores de conexión**, compruebe que está seleccionado **localhost. AdventureWorksDW2012**.  
  

## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 4: Adición de una tarea de flujo de datos al paquete](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Consulte también  
[Administrador de conexiones OLE DB](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
