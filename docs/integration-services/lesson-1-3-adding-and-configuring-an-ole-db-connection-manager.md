---
title: 'Paso 3: Agregar y configurar un administrador de conexiones OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4deede79c0e9be040c55cb2b8e4d00e3e3e4c6ca
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334239"
---
# <a name="lesson-1-3---adding-and-configuring-an-ole-db-connection-manager"></a>Lección 1-3: Agregar y configurar un administrador de conexiones OLE DB
Una vez que haya agregado un administrador de conexiones de archivos planos al origen de datos, la siguiente tarea consiste en agregar un administrador de conexiones OLE DB para conectarse al destino. Un administrador de conexiones OLE DB permite a un paquete extraer datos de un origen de datos compatible con OLE DB o cargar datos en este origen de datos. Mediante el administrador de conexiones OLE DB, puede especificar el servidor, el método de autenticación y la base de datos predeterminada de la conexión.  
  
En esta lección, creará un administrador de conexiones OLE DB que usa la Autenticación de Windows para conectarse a la instancia local de **AdventureWorksDB2012**. Otros componentes que creará más adelante en este tutorial, como la transformación Búsqueda y el destino de OLE DB, también harán referencia al administrador de conexiones OLE DB que cree.  
  
### <a name="add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>Agregar y configurar un administrador de conexiones de OLE DB para el paquete SSIS  
  
1.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y luego haga clic en **Nueva conexión OLE DB**.  
  
2.  En el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** , haga clic en **Nuevo**.  
  
3.  En **Nombre del servidor**, escriba **localhost**.  
  
    Cuando se especifica localhost como el nombre del servidor, el administración de conexión se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo local. Para usar una instancia remota de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sustituya localhost con el nombre del servidor al que desea conectarse.  
  
4.  En el grupo **Iniciar sesión en el servidor** , compruebe que la opción **Usar autenticación de Windows** está seleccionada.  
  
5.  En el grupo **Conectar con una base de datos** , en el cuadro **Seleccione o escriba un nombre de base de datos** , escriba o seleccione **AdventureWorksDW2012**.  
  
6.  Haga clic en **Probar conexión** para comprobar si los parámetros de conexión que ha especificado son válidos.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Haga clic en **Aceptar**.  
  
9. En el panel **Conexiones de datos** del cuadro de diálogo **Configurar el administrador de conexiones OLE DB** , compruebe que la opción **localhost.AdventureWorksDW2012** está seleccionada.  
  
10. Haga clic en **Aceptar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 4: agregar una tarea de flujo de datos al paquete](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Ver también  
[Administrador de conexiones OLE DB](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
