---
title: Ejecuta la aplicación de ejemplo de la libreta de direcciones | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34611cf13d72d962902bb6e143324d0c2771c1ab
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274304"
---
# <a name="running-the-address-book-sample-application"></a>Ejecuta la aplicación de ejemplo de la libreta de direcciones
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para ejecutar la aplicación de la libreta de direcciones, siga este procedimiento.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-run-this-application"></a>Para ejecutar esta aplicación  
  
1.  Asegúrese de que se está ejecutando Microsoft SQL Server. Haga clic en **iniciar**, seleccione **programas**, seleccione **Microsoft SQL Server 7.0**y, a continuación, haga clic en **Service Manager**. Si hay una flecha verde en el círculo blanco, se está ejecutando SQL Server. Si no lo es (habrá un cuadrado rojo en el círculo blanco), haga clic en **iniciar o continuar**.  
  
2.  En Microsoft Internet Explorer 4.0 o posterior, escriba la dirección siguiente:  
  
     **http://** *webserver* **/RDS/AddressBook/AddrBook.asp**  
  
     donde *webserver* es el nombre del servidor Web donde se instalan los componentes de servidor RDS.  
  
3.  A continuación, puede probar varios escenarios en la aplicación de ejemplo Libreta de direcciones, como buscar una persona en función de su nombre de correo electrónico, mostrar todas las personas con el título "Program Manager", o modificar registros existentes. Haga clic en **buscar** para rellenar la cuadrícula de datos con todos los nombres disponibles.  
  
## <a name="see-also"></a>Vea también  
 [Objeto de enlace de datos de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




