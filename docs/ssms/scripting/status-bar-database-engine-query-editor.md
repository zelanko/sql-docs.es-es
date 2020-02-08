---
title: Barra de estado (Editor de consultas del motor de base de datos)
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a579eeeb12795c76bbe585a982a159d6e069813d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243447"
---
# <a name="status-bar-database-engine-query-editor"></a>Barra de estado (Editor de consultas del motor de base de datos)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La barra de estado de las ventanas del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede codificarse por colores para indicar la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] a la que está conectada cada ventana.

1. **Antes de empezar:**  [Colores de la barra de estado](#StatusBarColors)  

2. **Para establecer un color de estado del servidor en:**  [Explorador de objetos](#SetOEServerColor), [Servidor registrado](#SetRegServerColor)  

3. **Para usar un color de estado:**  [Abrir el editor de consultas usando un color de servidor](#OpenServerColor), [Abrir un editor de consultas especificando un color de estado](#OpenSpecColor)  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

##  <a name="StatusBarColors"></a> Colores de la barra de estado

Puede asociar el color de una barra de estado con un determinado nodo del servidor en el **Explorador de objetos** o en los **Servidores registrados**. Los colores solo se pueden especificar en los nodos del servidor conectados a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], no en los nodos del servidor de otras tecnologías de SQL Server. También puede especificar un color personalizado para la barra de estado cada vez que conecte una nueva ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Puede abrir una ventana del Editor de consultas mediante el color de estado definido en el nodo de servidor o especificar un color único para la ventana del editor.  

Si desea establecer un color de barra de estado personalizado para un nodo de servidor en el Explorador de objetos, deberá hacerlo al realizar la conexión. Para cambiar el color asociado a un nodo de servidor existente, deberá desconectar y conectarse de nuevo especificando el nuevo color.  

##  <a name="SetOEServerColor"></a> Establecer el color de estado de un servidor en el Explorador de objetos

**Para establecer el color de estado del servidor en el Explorador de objetos**  
  
1.  En el **Explorador de objetos**, haga clic en el botón **Conectar** y después seleccione **Motor de base de datos...** .  
  
2.  En el cuadro de diálogo **Conectar con el servidor**, seleccione **Options >>** .  
  
3.  Active la casilla **Usar color personalizado** .  
  
4.  Para elegir el color, haga clic en el botón **Seleccionar…** .  
  
5.  Seleccione un color básico o personalizado y haga clic en Aceptar.  
  
6.  Complete el resto de la información de conexión y, a continuación, haga clic en el botón **Conectar** .  
  
##  <a name="SetRegServerColor"></a> Establecer el color de estado en un servidor registrado  
 **Para establecer el color de estado en un servidor registrado**  
  
1.  En **Servidores registrados**, haga clic con el botón derecho en el nodo de servidor y después haga clic en **Propiedades...** .  
  
2.  En el cuadro de diálogo **Editar propiedades de registro de servidor** , seleccione la pestaña **Propiedades de conexión** .  
  
3.  Active la casilla **Usar color personalizado** .  
  
4.  Para elegir el color, haga clic en el botón **Seleccionar…** .  
  
5.  Seleccione un color básico o personalizado y haga clic en Aceptar.  
  
6.  Haga clic en el botón **Guardar** del cuadro de diálogo **Editar propiedades de registro de servidor** .  
  
##  <a name="OpenServerColor"></a> Abrir un editor mediante un color de servidor  
 **Para abrir una ventana del editor mediante un color de servidor**  
  
-   Haga clic con el botón derecho en un nodo del servidor en el **Explorador de objetos** o en **Servidores registrados**y seleccione **Nueva consulta**.  
  
-   O bien, resalte un nodo servidor y, a continuación, haga clic en el botón de la barra de herramientas **Nueva consulta** .  
  
-   La barra de estado de la ventana del editor usará el color definido para el servidor asociado.  
  
##  <a name="OpenSpecColor"></a> Abrir un editor especificando un color de estado  
 **Para abrir una ventana del editor especificando un color de estado**  
  
-   Abra el menú **Archivo** , seleccione **Nuevo**y, a continuación, seleccione **Consulta de motor de base de datos**.  
  
-   En el cuadro de diálogo **Conectar con el servidor**, seleccione **Options >>** .  
  
-   Active la casilla **Usar color personalizado** .  
  
-   Para elegir el color, haga clic en el botón **Seleccionar…** .  
  
-   Seleccione un color básico o personalizado y haga clic en Aceptar.  
  
-   Complete el resto de la información de conexión y, a continuación, haga clic en el botón **Conectar** .  
  
## <a name="see-also"></a>Consulte también  
 [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
