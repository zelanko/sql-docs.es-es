---
title: Ejecutar el Script SQL de libreta de direcciones | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4751361a50f4fe594ad4ffc9d4233b41a4918361
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="running-the-address-book-sql-script"></a>Ejecutar el Script SQL de libreta de direcciones
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Debe usar la utilidad de línea de comandos del analizador de consultas o ISQL o el Administrador corporativo de SQL Server para ejecutar el script SQL incluye (Sampleemp.sql) que:  
  
-   Crea una nueva base de datos, AddrBookDB, en el dispositivo predeterminado.  
  
-   Se conecta a la base de datos, AddrBookDB.  
  
-   Crea una tabla de empleados.  
  
-   Rellena la tabla con datos de ejemplo.  
  
-   Se ejecuta una instrucción SELECT para comprobar el rellenado de la tabla de base de datos.  
  
-   Configura una cuenta de usuario denominada "adcdemo" con una contraseña de "adcdemo."  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Para ejecutar el script Sampleemp.sql en Microsoft SQL Server 6.5  
  
1.  Haga clic en **iniciar**, seleccione **programas**y, a continuación, seleccione **Microsoft SQL Server 6.5**. Haga clic en **Administrador corporativo de SQL**.  
  
2.  Desde el **herramientas** menú, haga clic en **herramienta de consulta SQL**.  
  
3.  Haga clic en **cargar secuencia de comandos SQL** y vaya a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Seleccione el archivo Sampleemp.sql. Haga clic en **Abrir**.  
  
5.  Haga clic en el **Ejecutar consulta** botón (la flecha verde en la barra de herramientas).  
  
6.  Una vez que se ejecuta, cierre el **consulta** y **Enterprise Manager** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Para ejecutar el script Sampleemp.sql en Microsoft SQL Server 7.0  
  
1.  Haga clic en **iniciar**, seleccione **programas**y, a continuación, seleccione **Microsoft SQL Server 7.0**. Haga clic en **Enterprise Manager**.  
  
2.  Asegúrese de que está seleccionado el servidor SQL Server que desea usar en la lista de servidores registrados en el Administrador corporativo.  
  
3.  Desde el **herramientas** menú, haga clic en **analizador de consultas de SQL Server**.  
  
4.  Haga clic en el **cargar secuencia de comandos SQL** botón (la carpeta abierta en la barra de herramientas) y vaya a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Seleccione el archivo Sampleemp.sql. Haga clic en **Abrir**.  
  
6.  Haga clic en el **Ejecutar consulta** botón (la flecha verde en la barra de herramientas) o **F5**.  
  
7.  Una vez que se ejecuta, cierre el **consulta**, **analizador de consultas**, y **Enterprise Manager** windows.  
  
## <a name="see-also"></a>Vea también  
 [Ejecuta la aplicación de ejemplo de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)



