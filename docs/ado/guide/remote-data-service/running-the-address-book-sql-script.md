---
title: Ejecutar el Script SQL de libreta de direcciones | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c77bece1b2ab67cc361f7445240e1a2b1190587
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51557802"
---
# <a name="running-the-address-book-sql-script"></a>Ejecución del script de SQL de la libreta de direcciones
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Debe usar la utilidad de línea de comandos del analizador de ISQL/consultas o el Administrador corporativo de SQL Server para ejecutar el script SQL incluye (Sampleemp.sql) que:  
  
-   Crea una nueva base de datos, AddrBookDB, en el dispositivo predeterminado.  
  
-   Se conecta a la base de datos, AddrBookDB.  
  
-   Crea una tabla de empleados.  
  
-   Rellena la tabla con datos de ejemplo.  
  
-   Se ejecuta una instrucción SELECT simple para comprobar el rellenado de la tabla de base de datos.  
  
-   Configura una cuenta de usuario denominada "adcdemo" con la contraseña "adcdemo."  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Para ejecutar el script Sampleemp.sql en Microsoft SQL Server 6.5  
  
1.  Haga clic en **iniciar**, apunte a **programas**y, a continuación, elija **Microsoft SQL Server 6.5**. Haga clic en **Administrador corporativo de SQL**.  
  
2.  Desde el **herramientas** menú, haga clic en **herramienta de consulta SQL**.  
  
3.  Haga clic en **carga SQL Script** y vaya a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Seleccione el archivo Sampleemp.sql. Haga clic en **Abrir**.  
  
5.  Haga clic en el **Ejecutar consulta** botón (la flecha verde en la barra de herramientas).  
  
6.  Una vez que se ejecuta, cierre el **consulta** y **Enterprise Manager** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Para ejecutar el script Sampleemp.sql en Microsoft SQL Server 7.0  
  
1.  Haga clic en **iniciar**, apunte a **programas**y, a continuación, elija **Microsoft SQL Server 7.0**. Haga clic en **Enterprise Manager**.  
  
2.  Asegúrese de que está seleccionado el servidor SQL Server que desea usar en la lista de servidores registrados en el Administrador corporativo.  
  
3.  Desde el **herramientas** menú, haga clic en **analizador de consultas de SQL Server**.  
  
4.  Haga clic en el **carga SQL Script** botón (Abrir carpeta en la barra de herramientas) y busque c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Seleccione el archivo Sampleemp.sql. Haga clic en **Abrir**.  
  
6.  Haga clic en el **Ejecutar consulta** botón (la flecha verde en la barra de herramientas) o **F5**.  
  
7.  Una vez que se ejecuta, cierre el **consulta**, **analizador de consultas**, y **Enterprise Manager** windows.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de la aplicación de ejemplo de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


