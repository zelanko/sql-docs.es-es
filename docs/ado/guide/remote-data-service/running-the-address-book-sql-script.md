---
description: Ejecución del script de SQL de la libreta de direcciones
title: Ejecutando el script SQL de la libreta de direcciones | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 17ea6bc39986239f0dc7c16c245bc08807b3f207
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451997"
---
# <a name="running-the-address-book-sql-script"></a>Ejecución del script de SQL de la libreta de direcciones
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Debe usar la utilidad de línea de comandos ISQL/Query Analyzer o el administrador de SQL Server Enterprise para ejecutar el script SQL incluido (Sampleemp. SQL) que:  
  
-   Crea una base de datos nueva, AddrBookDB, en el dispositivo predeterminado.  
  
-   Se conecta a la base de datos, AddrBookDB.  
  
-   Crea una tabla de empleados.  
  
-   Rellena la tabla con datos de ejemplo.  
  
-   Ejecuta una instrucción SELECT simple para comprobar el rellenado de la tabla de base de datos.  
  
-   Configura una cuenta de usuario denominada "adcdemo" con la contraseña "adcdemo".  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Para ejecutar el script Sampleemp. SQL en Microsoft SQL Server 6,5  
  
1.  Haga clic en **Inicio**, elija **programas**y, a continuación, seleccione **Microsoft SQL Server 6,5**. Haga clic en **Administrador corporativo de SQL**.  
  
2.  En el menú **herramientas** , haga clic en **herramienta de consulta SQL**.  
  
3.  Haga clic en **cargar script SQL** y vaya a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Seleccione el archivo Sampleemp. SQL. Haga clic en **Abrir**.  
  
5.  Haga clic en el botón **Ejecutar consulta** (la flecha verde en la barra de herramientas).  
  
6.  Una vez ejecutada, cierre las ventanas **consulta** y **Administrador corporativo** .  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Para ejecutar el script Sampleemp. SQL en Microsoft SQL Server 7,0  
  
1.  Haga clic en **Inicio**, elija **programas**y, a continuación, seleccione **Microsoft SQL Server 7,0**. Haga clic en **Administrador corporativo**.  
  
2.  Asegúrese de que la SQL Server que desea usar está seleccionada en la lista de servidores registrados en el Administrador corporativo.  
  
3.  En el menú **herramientas** , haga clic en **SQL Server analizador de consultas**.  
  
4.  Haga clic en el botón **cargar script SQL** (abrir carpeta en la barra de herramientas) y vaya a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Seleccione el archivo Sampleemp. SQL. Haga clic en **Abrir**.  
  
6.  Haga clic en el botón **Ejecutar consulta** (la flecha verde en la barra de herramientas) o **F5**.  
  
7.  Una vez ejecutada, cierre las ventanas **consulta**, **analizador de consultas**y **Administrador corporativo** .  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de la aplicación de ejemplo de la libreta de direcciones](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


