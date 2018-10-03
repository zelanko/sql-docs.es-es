---
title: Publicación de una base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9bb58b72cb4a4e785c4dc94b448e5e754ac0c80
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129745"
---
# <a name="publish-a-database-sql-server-management-studio"></a>Publicar una base de datos (SQL Server Management Studio)
  Puede usar el **Asistente Generar y publicar scripts** para publicar una base de datos completa u objetos de base de datos individuales en un proveedor de hospedaje web.  
  
> [!NOTE]  
>  La funcionalidad descrita en este tema solía proporcionarla el Asistente para publicar bases de datos. La funcionalidad de publicación se ha agregado al Asistente Generar y publicar scripts y el Asistente para publicar bases de datos ha desparecido.  
  
## <a name="generate-and-publish-scripts-wizard"></a>Asistente generar y publicar scripts  
 El Asistente Generar y publicar scripts puede usarse para publicar una base de datos u objetos seleccionados de una base de datos en un proveedor de hospedaje web. Un proveedor de hospedaje web de SQL Server es una interfaz de conectividad con un servicio web. El servicio web se crea usando el proyecto Database Publishing Services de SQL Server Hosting Toolkit en CodePlex. El servicio web facilita a los clientes del anfitrión web publicar sus bases de datos en el servicio usando el Asistente Generar y publicar scripts. Para obtener más información sobre cómo descargar el SQL Server Hosting Toolkit, vea [SQL Server Database Publishing Services](http://go.microsoft.com/fwlink/?LinkId=142025).  
  
 El Asistente Generar y publicar scripts también se puede usar para crear un script para transferir una base de datos.  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>Para publicar una base de datos en un servicio web  
  
1.  En el Explorador de objetos, expanda **Bases de datos**, haga clic con el botón derecho en una base de datos, seleccione **Tareas**y, después, haga clic en **Generar y publicar scripts**. Siga las instrucciones del asistente para incluir los objetos de la base de datos en el script para su publicación.  
  
2.  En la página **Elegir objetos** , seleccione los objetos que se van a publicar en el servicio de hospedaje web.  
  
3.  En la página **Establecer opciones de scripting** , seleccione **Publicar en servicio web**.  
  
    1.  En el cuadro **Proveedor** , especifique el proveedor para su servicio web. Si no ha configurado un proveedor de hospedaje web, seleccione **Proveedores administrados** y use el diálogo **Proveedores administrados** para configurar un proveedor para su servicio web.  
  
    2.  Para especificar opciones de publicación avanzadas, seleccione el botón **Avanzadas** en la sección **Publicar en servicio web** .  
  
4.  En la página **Resumen** , revise sus selecciones. Haga clic en **Anterior** para cambiar sus selecciones. Haga clic en **Siguiente** para publicar los objetos que seleccionó.  
  
5.  En la página **Guardar o publicar scripts** , supervise el progreso de la publicación.  
  
## <a name="see-also"></a>Vea también  
 [Generar scripts &#40;SQL Server Management Studio&#41;](../scripting/generate-scripts-sql-server-management-studio.md)   
 [Copiar bases de datos en otros servidores](copy-databases-to-other-servers.md)  
  
  
