---
title: Administrar objetos mediante el Explorador de objetos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d499666f51605e7df90332174c82681f8a386017
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75257218"
---
# <a name="manage-objects-by-using-object-explorer"></a>Administrar objetos mediante el Explorador de objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede utilizar el Explorador de objetos para administrar objetos, como bases de datos, tablas y procedimientos almacenados.  
  
## <a name="viewing-objects-in-object-explorer"></a>Ver objetos en el Explorador de objetos  
El Explorador de objetos utiliza una estructura de árbol para agrupar la información en carpetas. Para expandir las carpetas, haga clic en el signo más (+) o haga doble clic en la carpeta. Expanda las carpetas para obtener información más detallada. Haga clic con el botón secundario en las carpetas o en los objetos para realizar tareas comunes. Haga doble clic en los objetos para realizar las tareas más comunes.  
  
La primera vez que expanda una carpeta, el Explorador de objetos pedirá al servidor información para rellenar el árbol. Mientras el árbol se rellena, puede realizar otras funciones. Mientras el Explorador de objetos rellena el árbol, puede hacer clic en **Detener** para interrumpir el proceso. Otras acciones, como el filtrado de la lista, solo actuarán sobre la parte de la carpeta que esté rellena, a menos que se actualice la carpeta para volver a empezar a rellenar.  
  
Para conservar recursos cuando hay muchos objetos, las carpetas del árbol del Explorador de objetos no actualizan automáticamente su lista de contenido. Para actualizar la lista de objetos de una carpeta, haga clic con el botón derecho en esa carpeta y, a continuación, haga clic en **Actualizar**.  
  
El Explorador de objetos solamente puede mostrar hasta 65536 objetos. Una vez superada esta cifra, no es posible desplazarse por otros objetos en el árbol del Explorador de objetos. Para ver objetos adicionales en el Explorador de objetos, cierre aquellos nodos que no esté utilizando o aplique filtros para reducir el número de objetos.  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>Filtrar la lista de objetos en el Explorador de objetos  
Cuando una carpeta contiene un gran número de objetos, puede ser difícil encontrar el que se busca. En estos casos, utilice la característica de filtro del Explorador de objetos a fin de reducir la lista. Por ejemplo, quizás desee buscar un usuario de una base de datos concreta o la última tabla creada en listas que contienen cientos de objetos. Haga clic en la carpeta que desea filtrar y, a continuación, en el botón de filtro para abrir el cuadro de diálogo **Configuración del filtro** . Es posible filtrar la lista por nombre, fecha de creación y, algunas veces, por esquema, así como proporcionar operadores de filtrado adicionales como **Empieza por**, **Contiene**y **Entre**.  
  
## <a name="multi-select"></a>Selección múltiple  
El Explorador de objetos solamente permite seleccionar un objeto cada vez. Para seleccionar varios elementos, presione **F7** para abrir la página **Detalles del Explorador de objetos**. La página **Detalles del Explorador de objetos** admite la selección múltiple.  
  
## <a name="register-a-server-from-object-explorer"></a>Registrar un servidor del Explorador de objetos  
Una vez conectado a un servidor, es muy sencillo registrar ese servidor para su uso posterior. En el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y, a continuación, haga clic en **Registrar**. En el cuadro de diálogo **Registrar servidor** , especifique en qué lugar del árbol del grupo de servidores desea colocar ese servidor. En el cuadro **Nombre del servidor** , puede sustituir el nombre del servidor por otro más explicativo. Por ejemplo, puede registrar el servidor **APSQL02** con un nombre más descriptivo, como "**Cuentas por pagar**".  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>Ejecutar acciones en nodos del Explorador de objetos  
Las acciones se llevan a cabo en los objetos haciendo clic con el botón secundario en el nodo del Explorador de objetos que representa el objeto. Cada tipo de objeto admite un conjunto único de acciones del botón secundario. Algunos de los tipos de acciones que puede realizar con los menús del botón secundario son:  
  
### <a name="open-a-connected-query-editor"></a>Abrir un Editor de consultas conectado  
Cuando el Explorador de objetos está conectado a un servidor, es posible abrir una ventana nueva del Editor de código mediante los valores de conexión del Explorador de objetos. Para abrir una ventana nueva del Editor de código, haga clic con el botón derecho en el nombre del servidor en el Explorador de objetos y, a continuación, haga clic en **Nueva consulta**. Para abrir una ventana del Editor de código mediante una base de datos concreta, haga clic con el botón derecho en el nombre del servidor y, a continuación, haga clic en **Nueva consulta**. Al abrir una consulta nueva para un servidor de Analysis Services, puede seleccionar consultas DMX, MDX o XMLA.  
  
### <a name="start-powershell"></a>Iniciar PowerShell  
Puede iniciar una sesión de PowerShell haciendo clic con el botón derecho en la mayoría de las carpetas y objetos en el árbol del Explorador de objetos y seleccionando **Iniciar PowerShell**. De este modo se inicia una sesión de PowerShell que tiene habilitada la compatibilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, y tiene establecida la ruta de acceso al objeto en el que hizo clic con el botón secundario en el Explorador de objetos. A continuación, puede escribir comandos de PowerShell en un entorno interactivo de PowerShell. Para más información, consulte el artículo sobre [SQL Server PowerShell](https://msdn.microsoft.com/89b70725-bbe7-4ffe-a27d-2a40005a97e7).  
  
## <a name="see-also"></a>Consulte también  
[Explorador de objetos](../../ssms/object/object-explorer.md)  
[Abrir y configurar el Explorador de objetos](../../ssms/object/open-and-configure-object-explorer.md)  
[Conectarse a una instancia desde el Explorador de objetos](../../ssms/object/connect-to-an-instance-from-object-explorer.md)  
[Panel Detalles del Explorador de objetos](../../ssms/object/object-explorer-details-pane.md)  
[Informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
  
